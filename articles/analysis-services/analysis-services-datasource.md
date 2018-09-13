---
title: Datasource connections | Microsoft Docs
description: Describes data source connections for data models in Azure Analysis Services.
services: analysis-services
documentationcenter: ''
author: minewiskan
manager: erikre
editor: ''
tags: ''
ms.assetid: 6ec63319-ff9b-4b01-a1cd-274481dc8995
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 04/14/2017
ms.author: owend
ms.openlocfilehash: b396e2bbaa075a735bb474b428a91a5dfe3a341a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662687"
---
# <a name="datasource-connections"></a><span data-ttu-id="05a2e-103">Datasource connections</span><span class="sxs-lookup"><span data-stu-id="05a2e-103">Datasource connections</span></span>
<span data-ttu-id="05a2e-104">Data models in Azure Analysis Services may require different data providers when connecting to certain data sources.</span><span class="sxs-lookup"><span data-stu-id="05a2e-104">Data models in Azure Analysis Services may require different data providers when connecting to certain data sources.</span></span> <span data-ttu-id="05a2e-105">In some cases, tabular models connecting to data sources using native providers such as SQL Server Native Client (SQLNCLI11) may return an error.</span><span class="sxs-lookup"><span data-stu-id="05a2e-105">In some cases, tabular models connecting to data sources using native providers such as SQL Server Native Client (SQLNCLI11) may return an error.</span></span>

<span data-ttu-id="05a2e-106">For example; if you have an in-memory or Direct Query data model that connects to a cloud data source such as Azure SQL Database, if you use native providers other than SQLOLEDB, you may see error message: **“The provider 'SQLNCLI11.1' is not registered”**.</span><span class="sxs-lookup"><span data-stu-id="05a2e-106">For example; if you have an in-memory or Direct Query data model that connects to a cloud data source such as Azure SQL Database, if you use native providers other than SQLOLEDB, you may see error message: **“The provider 'SQLNCLI11.1' is not registered”**.</span></span>

<span data-ttu-id="05a2e-107">Or, if you have a DirectQuery model connecting to on-premises data sources, if you use native providers you may see error message: **“Error creating OLE DB row set. Incorrect syntax near 'LIMIT'”**.</span><span class="sxs-lookup"><span data-stu-id="05a2e-107">Or, if you have a DirectQuery model connecting to on-premises data sources, if you use native providers you may see error message: **“Error creating OLE DB row set. Incorrect syntax near 'LIMIT'”**.</span></span>

## <a name="data-source-providers"></a><span data-ttu-id="05a2e-108">Data source providers</span><span class="sxs-lookup"><span data-stu-id="05a2e-108">Data source providers</span></span>
<span data-ttu-id="05a2e-109">The following datasource providers are supported for in-memory or Direct Query data models when connecting to data sources in the cloud or on-premises:</span><span class="sxs-lookup"><span data-stu-id="05a2e-109">The following datasource providers are supported for in-memory or Direct Query data models when connecting to data sources in the cloud or on-premises:</span></span>

### <a name="cloud"></a><span data-ttu-id="05a2e-110">Cloud</span><span class="sxs-lookup"><span data-stu-id="05a2e-110">Cloud</span></span>
| <span data-ttu-id="05a2e-111">**Datasource**</span><span class="sxs-lookup"><span data-stu-id="05a2e-111">**Datasource**</span></span> | <span data-ttu-id="05a2e-112">**In-memory**</span><span class="sxs-lookup"><span data-stu-id="05a2e-112">**In-memory**</span></span> | <span data-ttu-id="05a2e-113">**Direct Query**</span><span class="sxs-lookup"><span data-stu-id="05a2e-113">**Direct Query**</span></span> |
|  --- | --- | --- |
| <span data-ttu-id="05a2e-114">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="05a2e-114">Azure SQL Data Warehouse</span></span> |<span data-ttu-id="05a2e-115">.NET Framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="05a2e-115">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="05a2e-116">.NET Framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="05a2e-116">.NET Framework Data Provider for SQL Server</span></span> |
| <span data-ttu-id="05a2e-117">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="05a2e-117">Azure SQL Database</span></span> |<span data-ttu-id="05a2e-118">.NET Framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="05a2e-118">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="05a2e-119">.NET Framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="05a2e-119">.NET Framework Data Provider for SQL Server</span></span> | |

### <a name="on-premises-via-gateway"></a><span data-ttu-id="05a2e-120">On-premises (via Gateway)</span><span class="sxs-lookup"><span data-stu-id="05a2e-120">On-premises (via Gateway)</span></span>
|<span data-ttu-id="05a2e-121">**Datasource**</span><span class="sxs-lookup"><span data-stu-id="05a2e-121">**Datasource**</span></span> | <span data-ttu-id="05a2e-122">**In-memory**</span><span class="sxs-lookup"><span data-stu-id="05a2e-122">**In-memory**</span></span> | <span data-ttu-id="05a2e-123">**Direct Query**</span><span class="sxs-lookup"><span data-stu-id="05a2e-123">**Direct Query**</span></span> |
|  --- | --- | --- |
| <span data-ttu-id="05a2e-124">SQL Server</span><span class="sxs-lookup"><span data-stu-id="05a2e-124">SQL Server</span></span> |<span data-ttu-id="05a2e-125">SQL Server Native Client 11.0</span><span class="sxs-lookup"><span data-stu-id="05a2e-125">SQL Server Native Client 11.0</span></span> |<span data-ttu-id="05a2e-126">.NET Framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="05a2e-126">.NET Framework Data Provider for SQL Server</span></span> |
| <span data-ttu-id="05a2e-127">SQL Server</span><span class="sxs-lookup"><span data-stu-id="05a2e-127">SQL Server</span></span> |<span data-ttu-id="05a2e-128">Microsoft OLE DB Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="05a2e-128">Microsoft OLE DB Provider for SQL Server</span></span> |<span data-ttu-id="05a2e-129">.NET Framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="05a2e-129">.NET Framework Data Provider for SQL Server</span></span> | |
| <span data-ttu-id="05a2e-130">SQL Server</span><span class="sxs-lookup"><span data-stu-id="05a2e-130">SQL Server</span></span> |<span data-ttu-id="05a2e-131">.NET Framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="05a2e-131">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="05a2e-132">.NET Framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="05a2e-132">.NET Framework Data Provider for SQL Server</span></span> | |
| <span data-ttu-id="05a2e-133">Oracle</span><span class="sxs-lookup"><span data-stu-id="05a2e-133">Oracle</span></span> |<span data-ttu-id="05a2e-134">Microsoft OLE DB Provider for Oracle</span><span class="sxs-lookup"><span data-stu-id="05a2e-134">Microsoft OLE DB Provider for Oracle</span></span> |<span data-ttu-id="05a2e-135">Oracle Data Provider for .NET</span><span class="sxs-lookup"><span data-stu-id="05a2e-135">Oracle Data Provider for .NET</span></span> | |
| <span data-ttu-id="05a2e-136">Oracle</span><span class="sxs-lookup"><span data-stu-id="05a2e-136">Oracle</span></span> |<span data-ttu-id="05a2e-137">Oracle Data Provider for .NET</span><span class="sxs-lookup"><span data-stu-id="05a2e-137">Oracle Data Provider for .NET</span></span> |<span data-ttu-id="05a2e-138">Oracle Data Provider for .NET</span><span class="sxs-lookup"><span data-stu-id="05a2e-138">Oracle Data Provider for .NET</span></span> | |
| <span data-ttu-id="05a2e-139">Teradata</span><span class="sxs-lookup"><span data-stu-id="05a2e-139">Teradata</span></span> |<span data-ttu-id="05a2e-140">OLE DB Provider for Teradata</span><span class="sxs-lookup"><span data-stu-id="05a2e-140">OLE DB Provider for Teradata</span></span> |<span data-ttu-id="05a2e-141">Teradata Data Provider for .NET</span><span class="sxs-lookup"><span data-stu-id="05a2e-141">Teradata Data Provider for .NET</span></span> | |
| <span data-ttu-id="05a2e-142">Teradata</span><span class="sxs-lookup"><span data-stu-id="05a2e-142">Teradata</span></span> |<span data-ttu-id="05a2e-143">Teradata Data Provider for .NET</span><span class="sxs-lookup"><span data-stu-id="05a2e-143">Teradata Data Provider for .NET</span></span> |<span data-ttu-id="05a2e-144">Teradata Data Provider for .NET</span><span class="sxs-lookup"><span data-stu-id="05a2e-144">Teradata Data Provider for .NET</span></span> | |
| <span data-ttu-id="05a2e-145">Analytics Platform System</span><span class="sxs-lookup"><span data-stu-id="05a2e-145">Analytics Platform System</span></span> |<span data-ttu-id="05a2e-146">.NET Framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="05a2e-146">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="05a2e-147">.NET Framework Data Provider for SQL Server</span><span class="sxs-lookup"><span data-stu-id="05a2e-147">.NET Framework Data Provider for SQL Server</span></span> | |

> [!NOTE]
> <span data-ttu-id="05a2e-148">Ensure 64-bit providers are installed when using On-premises gateway.</span><span class="sxs-lookup"><span data-stu-id="05a2e-148">Ensure 64-bit providers are installed when using On-premises gateway.</span></span>
> 
> 

<span data-ttu-id="05a2e-149">When migrating an on-premises SQL Server Analysis Services tabular model to Azure Analysis Services, it may be necessary to change the provider.</span><span class="sxs-lookup"><span data-stu-id="05a2e-149">When migrating an on-premises SQL Server Analysis Services tabular model to Azure Analysis Services, it may be necessary to change the provider.</span></span>

<span data-ttu-id="05a2e-150">**To specify a datasource provider**</span><span class="sxs-lookup"><span data-stu-id="05a2e-150">**To specify a datasource provider**</span></span>

1. <span data-ttu-id="05a2e-151">In SSDT > **Tabular Model Explorer** > **Data Sources**, right-click a data source connection, and then click **Edit Data Source**.</span><span class="sxs-lookup"><span data-stu-id="05a2e-151">In SSDT > **Tabular Model Explorer** > **Data Sources**, right-click a data source connection, and then click **Edit Data Source**.</span></span>
2. <span data-ttu-id="05a2e-152">In **Edit Connection**, click **Advanced** to open the Advance properties window.</span><span class="sxs-lookup"><span data-stu-id="05a2e-152">In **Edit Connection**, click **Advanced** to open the Advance properties window.</span></span>
3. <span data-ttu-id="05a2e-153">In **Set Advanced Properties** > **Providers**, then select the appropriate provider.</span><span class="sxs-lookup"><span data-stu-id="05a2e-153">In **Set Advanced Properties** > **Providers**, then select the appropriate provider.</span></span>

## <a name="impersonation"></a><span data-ttu-id="05a2e-154">Impersonation</span><span class="sxs-lookup"><span data-stu-id="05a2e-154">Impersonation</span></span>
<span data-ttu-id="05a2e-155">In some cases, it may be necessary to specify a different impersonation account.</span><span class="sxs-lookup"><span data-stu-id="05a2e-155">In some cases, it may be necessary to specify a different impersonation account.</span></span> <span data-ttu-id="05a2e-156">Impersonation account can be specified in SSDT or SSMS.</span><span class="sxs-lookup"><span data-stu-id="05a2e-156">Impersonation account can be specified in SSDT or SSMS.</span></span>

<span data-ttu-id="05a2e-157">For on-premises data sources:</span><span class="sxs-lookup"><span data-stu-id="05a2e-157">For on-premises data sources:</span></span>

* <span data-ttu-id="05a2e-158">If using SQL authentication, impersonation should be Service Account.</span><span class="sxs-lookup"><span data-stu-id="05a2e-158">If using SQL authentication, impersonation should be Service Account.</span></span>
* <span data-ttu-id="05a2e-159">If using Windows authentication, set Windows user/password.</span><span class="sxs-lookup"><span data-stu-id="05a2e-159">If using Windows authentication, set Windows user/password.</span></span> <span data-ttu-id="05a2e-160">For SQL Server, Windows authentication with a specific impersonation account is supported only for in-memory data models.</span><span class="sxs-lookup"><span data-stu-id="05a2e-160">For SQL Server, Windows authentication with a specific impersonation account is supported only for in-memory data models.</span></span>

<span data-ttu-id="05a2e-161">For cloud data sources:</span><span class="sxs-lookup"><span data-stu-id="05a2e-161">For cloud data sources:</span></span>

* <span data-ttu-id="05a2e-162">If using SQL authentication, impersonation should be Service Account.</span><span class="sxs-lookup"><span data-stu-id="05a2e-162">If using SQL authentication, impersonation should be Service Account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05a2e-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="05a2e-163">Next steps</span></span>
<span data-ttu-id="05a2e-164">If you have on-premises data sources, be sure to install the [On-premises gateway](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="05a2e-164">If you have on-premises data sources, be sure to install the [On-premises gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="05a2e-165">To learn more about managing your server in SSDT or SSMS, see [Manage your server](analysis-services-manage.md).</span><span class="sxs-lookup"><span data-stu-id="05a2e-165">To learn more about managing your server in SSDT or SSMS, see [Manage your server](analysis-services-manage.md).</span></span>

