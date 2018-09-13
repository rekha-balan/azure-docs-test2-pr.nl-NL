---
title: Azure Government Databases | Microsoft Docs
description: This provides a comparision of features and guidance on developing applications for Azure Government
services: azure-government
cloud: gov
documentationcenter: ''
author: ryansoc
manager: zakramer
ms.assetid: a1e173a9-996a-4091-a2e3-6b1e36da9ae1
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 11/14/2016
ms.author: ryansoc
ms.openlocfilehash: 30287552ad85cd4fd7aa1a3ac249db7c20b47cf5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669263"
---
# <a name="azure-government-databases"></a><span data-ttu-id="82655-103">Azure Government Databases</span><span class="sxs-lookup"><span data-stu-id="82655-103">Azure Government Databases</span></span>
## <a name="sql-database"></a><span data-ttu-id="82655-104">SQL Database</span><span class="sxs-lookup"><span data-stu-id="82655-104">SQL Database</span></span>
<span data-ttu-id="82655-105">Refer to the<a href="https://msdn.microsoft.com/en-us/library/bb510589.aspx"> Microsoft Security Center for SQL Database Engine </a> and [Azure SQL Database Public Documentation](../sql-database/index.md) for additional guidance on metadata visibility configuration, and protection best practices.</span><span class="sxs-lookup"><span data-stu-id="82655-105">Refer to the<a href="https://msdn.microsoft.com/en-us/library/bb510589.aspx"> Microsoft Security Center for SQL Database Engine </a> and [Azure SQL Database Public Documentation](../sql-database/index.md) for additional guidance on metadata visibility configuration, and protection best practices.</span></span>

### <a name="variations"></a><span data-ttu-id="82655-106">Variations</span><span class="sxs-lookup"><span data-stu-id="82655-106">Variations</span></span>
<span data-ttu-id="82655-107">SQL V12 Database is generally available in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="82655-107">SQL V12 Database is generally available in Azure Government.</span></span>

<span data-ttu-id="82655-108">The Address for SQL Azure Servers in Azure Government is different:</span><span class="sxs-lookup"><span data-stu-id="82655-108">The Address for SQL Azure Servers in Azure Government is different:</span></span>

| <span data-ttu-id="82655-109">Service Type</span><span class="sxs-lookup"><span data-stu-id="82655-109">Service Type</span></span> | <span data-ttu-id="82655-110">Azure Public</span><span class="sxs-lookup"><span data-stu-id="82655-110">Azure Public</span></span> | <span data-ttu-id="82655-111">Azure Government</span><span class="sxs-lookup"><span data-stu-id="82655-111">Azure Government</span></span> |
| --- | --- | --- |
| <span data-ttu-id="82655-112">SQL Database</span><span class="sxs-lookup"><span data-stu-id="82655-112">SQL Database</span></span> |<span data-ttu-id="82655-113">\*.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="82655-113">\*.database.windows.net</span></span> |<span data-ttu-id="82655-114">\*.database.usgovcloudapi.net</span><span class="sxs-lookup"><span data-stu-id="82655-114">\*.database.usgovcloudapi.net</span></span> |

### <a name="considerations"></a><span data-ttu-id="82655-115">Considerations</span><span class="sxs-lookup"><span data-stu-id="82655-115">Considerations</span></span>
<span data-ttu-id="82655-116">The following information identifies the Azure Government boundary for Azure SQL:</span><span class="sxs-lookup"><span data-stu-id="82655-116">The following information identifies the Azure Government boundary for Azure SQL:</span></span>

| <span data-ttu-id="82655-117">Regulated/controlled data permitted</span><span class="sxs-lookup"><span data-stu-id="82655-117">Regulated/controlled data permitted</span></span> | <span data-ttu-id="82655-118">Regulated/controlled data not permitted</span><span class="sxs-lookup"><span data-stu-id="82655-118">Regulated/controlled data not permitted</span></span> |
| --- | --- |
| <span data-ttu-id="82655-119">All data stored and processed in Microsoft Azure SQL can contain Azure Government-regulated data.</span><span class="sxs-lookup"><span data-stu-id="82655-119">All data stored and processed in Microsoft Azure SQL can contain Azure Government-regulated data.</span></span> <span data-ttu-id="82655-120">You must use database tools for data transfer of Azure Government-regulated data.</span><span class="sxs-lookup"><span data-stu-id="82655-120">You must use database tools for data transfer of Azure Government-regulated data.</span></span> |<span data-ttu-id="82655-121">Azure SQL metadata is not permitted to contain export controlled data.</span><span class="sxs-lookup"><span data-stu-id="82655-121">Azure SQL metadata is not permitted to contain export controlled data.</span></span> <span data-ttu-id="82655-122">This metadata includes all configuration data entered when creating and maintaining your storage product.</span><span class="sxs-lookup"><span data-stu-id="82655-122">This metadata includes all configuration data entered when creating and maintaining your storage product.</span></span>  <span data-ttu-id="82655-123">Do not enter regulated/controlled data into the following fields: Database name, Subscription name, Resource groups, Server name, Server admin login, Deployment names, Resource names, Resource tags</span><span class="sxs-lookup"><span data-stu-id="82655-123">Do not enter regulated/controlled data into the following fields: Database name, Subscription name, Resource groups, Server name, Server admin login, Deployment names, Resource names, Resource tags</span></span> |

## <a name="azure-redis-cache"></a><span data-ttu-id="82655-124">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="82655-124">Azure Redis Cache</span></span>
<span data-ttu-id="82655-125">For details on this service and how to use it, see [Azure Redis Cache public documentation](../redis-cache/index.md).</span><span class="sxs-lookup"><span data-stu-id="82655-125">For details on this service and how to use it, see [Azure Redis Cache public documentation](../redis-cache/index.md).</span></span>

### <a name="variations"></a><span data-ttu-id="82655-126">Variations</span><span class="sxs-lookup"><span data-stu-id="82655-126">Variations</span></span>
<span data-ttu-id="82655-127">The URLs for accessing and managing Azure Redis Cache in Azure Government are different:</span><span class="sxs-lookup"><span data-stu-id="82655-127">The URLs for accessing and managing Azure Redis Cache in Azure Government are different:</span></span>

| <span data-ttu-id="82655-128">Service Type</span><span class="sxs-lookup"><span data-stu-id="82655-128">Service Type</span></span> | <span data-ttu-id="82655-129">Azure Public</span><span class="sxs-lookup"><span data-stu-id="82655-129">Azure Public</span></span> | <span data-ttu-id="82655-130">Azure Government</span><span class="sxs-lookup"><span data-stu-id="82655-130">Azure Government</span></span> |
| --- | --- | --- |
| <span data-ttu-id="82655-131">Cache endpoint</span><span class="sxs-lookup"><span data-stu-id="82655-131">Cache endpoint</span></span> |<span data-ttu-id="82655-132">\*.redis.cache.windows.net</span><span class="sxs-lookup"><span data-stu-id="82655-132">\*.redis.cache.windows.net</span></span> |<span data-ttu-id="82655-133">\*.redis.cache.usgovcloudapi.net</span><span class="sxs-lookup"><span data-stu-id="82655-133">\*.redis.cache.usgovcloudapi.net</span></span> |
| <span data-ttu-id="82655-134">Azure portal</span><span class="sxs-lookup"><span data-stu-id="82655-134">Azure portal</span></span> |https://portal.azure.com |https://portal.azure.us |

> [!NOTE]
> <span data-ttu-id="82655-135">All of your scripts and code needs to account for the appropriate endpoints and environments.</span><span class="sxs-lookup"><span data-stu-id="82655-135">All of your scripts and code needs to account for the appropriate endpoints and environments.</span></span> <span data-ttu-id="82655-136">For more information, see [How to connect to other clouds](../redis-cache/cache-howto-manage-redis-cache-powershell.md#how-to-connect-to-other-clouds).</span><span class="sxs-lookup"><span data-stu-id="82655-136">For more information, see [How to connect to other clouds](../redis-cache/cache-howto-manage-redis-cache-powershell.md#how-to-connect-to-other-clouds).</span></span>
> 
> 

### <a name="considerations"></a><span data-ttu-id="82655-137">Considerations</span><span class="sxs-lookup"><span data-stu-id="82655-137">Considerations</span></span>
<span data-ttu-id="82655-138">The following information identifies the Azure Government boundary for Azure Redis Cache:</span><span class="sxs-lookup"><span data-stu-id="82655-138">The following information identifies the Azure Government boundary for Azure Redis Cache:</span></span>

| <span data-ttu-id="82655-139">Regulated/controlled data permitted</span><span class="sxs-lookup"><span data-stu-id="82655-139">Regulated/controlled data permitted</span></span> | <span data-ttu-id="82655-140">Regulated/controlled data not permitted</span><span class="sxs-lookup"><span data-stu-id="82655-140">Regulated/controlled data not permitted</span></span> |
| --- | --- |
| <span data-ttu-id="82655-141">All data stored and processed in Azure Redis Cache can contain Azure Government-regulated data.</span><span class="sxs-lookup"><span data-stu-id="82655-141">All data stored and processed in Azure Redis Cache can contain Azure Government-regulated data.</span></span> |<span data-ttu-id="82655-142">Azure Redis Cache metadata is not permitted to contain export controlled data.</span><span class="sxs-lookup"><span data-stu-id="82655-142">Azure Redis Cache metadata is not permitted to contain export controlled data.</span></span> <span data-ttu-id="82655-143">Do not enter regulated/controlled data into the following fields: Cache name, VNET name, Subscription name, Resource groups, Resource tags, Redis properties.</span><span class="sxs-lookup"><span data-stu-id="82655-143">Do not enter regulated/controlled data into the following fields: Cache name, VNET name, Subscription name, Resource groups, Resource tags, Redis properties.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="82655-144">Next Steps</span><span class="sxs-lookup"><span data-stu-id="82655-144">Next Steps</span></span>
<span data-ttu-id="82655-145">For supplemental information and updates subscribe to the <a href="https://blogs.msdn.microsoft.com/azuregov/">Microsoft Azure Government Blog. </a></span><span class="sxs-lookup"><span data-stu-id="82655-145">For supplemental information and updates subscribe to the <a href="https://blogs.msdn.microsoft.com/azuregov/">Microsoft Azure Government Blog. </a></span></span>

