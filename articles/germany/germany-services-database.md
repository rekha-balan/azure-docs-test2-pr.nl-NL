---
title: Azure Germany database services | Microsoft Docs
description: Provides a comparison of database services for Azure Germany
services: germany
cloud: na
documentationcenter: na
author: gitralf
manager: rainerst
ms.assetid: na
ms.service: germany
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/13/2017
ms.author: ralfwi
ms.openlocfilehash: f409f70a49e4592bc5fd83a0f8c9fb9311e6371b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869047"
---
# <a name="azure-germany-database-services"></a><span data-ttu-id="7077e-103">Azure Germany database services</span><span class="sxs-lookup"><span data-stu-id="7077e-103">Azure Germany database services</span></span>
## <a name="sql-database"></a><span data-ttu-id="7077e-104">SQL Database</span><span class="sxs-lookup"><span data-stu-id="7077e-104">SQL Database</span></span>
<span data-ttu-id="7077e-105">Azure SQL Database V12 is generally available in Azure Germany.</span><span class="sxs-lookup"><span data-stu-id="7077e-105">Azure SQL Database V12 is generally available in Azure Germany.</span></span> <span data-ttu-id="7077e-106">For guidance on metadata visibility configuration and protection best practices, see the [Microsoft Security Center for SQL Database Engine](https://msdn.microsoft.com/library/bb510589.aspx) and the [SQL Database global documentation](../sql-database/index.yml).</span><span class="sxs-lookup"><span data-stu-id="7077e-106">For guidance on metadata visibility configuration and protection best practices, see the [Microsoft Security Center for SQL Database Engine](https://msdn.microsoft.com/library/bb510589.aspx) and the [SQL Database global documentation](../sql-database/index.yml).</span></span>

### <a name="variations"></a><span data-ttu-id="7077e-107">Variations</span><span class="sxs-lookup"><span data-stu-id="7077e-107">Variations</span></span>
<span data-ttu-id="7077e-108">The address for SQL Database in Azure Germany is different from the address in global Azure:</span><span class="sxs-lookup"><span data-stu-id="7077e-108">The address for SQL Database in Azure Germany is different from the address in global Azure:</span></span>

| <span data-ttu-id="7077e-109">Service type</span><span class="sxs-lookup"><span data-stu-id="7077e-109">Service type</span></span> | <span data-ttu-id="7077e-110">Global Azure</span><span class="sxs-lookup"><span data-stu-id="7077e-110">Global Azure</span></span> | <span data-ttu-id="7077e-111">Azure Germany</span><span class="sxs-lookup"><span data-stu-id="7077e-111">Azure Germany</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7077e-112">SQL Database</span><span class="sxs-lookup"><span data-stu-id="7077e-112">SQL Database</span></span> | <span data-ttu-id="7077e-113">\*.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="7077e-113">\*.database.windows.net</span></span> | <span data-ttu-id="7077e-114">\*.database.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="7077e-114">\*.database.cloudapi.de</span></span> |


## <a name="azure-redis-cache"></a><span data-ttu-id="7077e-115">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="7077e-115">Azure Redis Cache</span></span>
<span data-ttu-id="7077e-116">For details on Azure Redis Cache and how to use it, see [Azure Redis Cache global documentation](../redis-cache/index.md).</span><span class="sxs-lookup"><span data-stu-id="7077e-116">For details on Azure Redis Cache and how to use it, see [Azure Redis Cache global documentation](../redis-cache/index.md).</span></span>

### <a name="variations"></a><span data-ttu-id="7077e-117">Variations</span><span class="sxs-lookup"><span data-stu-id="7077e-117">Variations</span></span>
<span data-ttu-id="7077e-118">The URLs for accessing and managing Azure Redis Cache in Azure Germany are different from the URLs in global Azure:</span><span class="sxs-lookup"><span data-stu-id="7077e-118">The URLs for accessing and managing Azure Redis Cache in Azure Germany are different from the URLs in global Azure:</span></span>

| <span data-ttu-id="7077e-119">Service type</span><span class="sxs-lookup"><span data-stu-id="7077e-119">Service type</span></span> | <span data-ttu-id="7077e-120">Global Azure</span><span class="sxs-lookup"><span data-stu-id="7077e-120">Global Azure</span></span> | <span data-ttu-id="7077e-121">Azure Germany</span><span class="sxs-lookup"><span data-stu-id="7077e-121">Azure Germany</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7077e-122">Cache endpoint</span><span class="sxs-lookup"><span data-stu-id="7077e-122">Cache endpoint</span></span> | <span data-ttu-id="7077e-123">\*.redis.cache.windows.net</span><span class="sxs-lookup"><span data-stu-id="7077e-123">\*.redis.cache.windows.net</span></span> | <span data-ttu-id="7077e-124">\*.redis.cache.cloudapi.de</span><span class="sxs-lookup"><span data-stu-id="7077e-124">\*.redis.cache.cloudapi.de</span></span> |
| <span data-ttu-id="7077e-125">Azure portal</span><span class="sxs-lookup"><span data-stu-id="7077e-125">Azure portal</span></span> | https://portal.azure.com | https://portal.microsoftazure.de |

> [!NOTE]
> <span data-ttu-id="7077e-126">All your scripts and code need to account for the appropriate endpoints and environments.</span><span class="sxs-lookup"><span data-stu-id="7077e-126">All your scripts and code need to account for the appropriate endpoints and environments.</span></span> <span data-ttu-id="7077e-127">For more information, see "To connect to Microsoft Azure Germany" in [Manage Azure Redis Cache with Azure PowerShell](../redis-cache/cache-howto-manage-redis-cache-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7077e-127">For more information, see "To connect to Microsoft Azure Germany" in [Manage Azure Redis Cache with Azure PowerShell](../redis-cache/cache-howto-manage-redis-cache-powershell.md).</span></span>
>
>


## <a name="next-steps"></a><span data-ttu-id="7077e-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="7077e-128">Next steps</span></span>
<span data-ttu-id="7077e-129">For supplemental information and updates, subscribe to the [Azure Germany blog](https://blogs.msdn.microsoft.com/azuregermany/).</span><span class="sxs-lookup"><span data-stu-id="7077e-129">For supplemental information and updates, subscribe to the [Azure Germany blog](https://blogs.msdn.microsoft.com/azuregermany/).</span></span>
