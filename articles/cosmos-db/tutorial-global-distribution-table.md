---
title: Azure Cosmos DB global distribution tutorial for Table API | Microsoft Docs
description: Learn how to set up Azure Cosmos DB global distribution using the Table API.
services: cosmos-db
keywords: global distribution, Table
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-table
ms.devlang: na
ms.topic: tutorial
ms.date: 12/13/2017
ms.author: sngun
ms.custom: mvc
ms.openlocfilehash: 4073d88ccb5350f4c5b209e61040dae35c2685b1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870381"
---
# <a name="set-up-azure-cosmos-db-global-distribution-using-the-table-api"></a><span data-ttu-id="b4194-104">Set up Azure Cosmos DB global distribution using the Table API</span><span class="sxs-lookup"><span data-stu-id="b4194-104">Set up Azure Cosmos DB global distribution using the Table API</span></span>

<span data-ttu-id="b4194-105">This article covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="b4194-105">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="b4194-106">Configure global distribution using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b4194-106">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="b4194-107">Configure global distribution using the [Table API](table-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="b4194-107">Configure global distribution using the [Table API](table-introduction.md)</span></span>

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-table-api"></a><span data-ttu-id="b4194-108">Connecting to a preferred region using the Table API</span><span class="sxs-lookup"><span data-stu-id="b4194-108">Connecting to a preferred region using the Table API</span></span>

<span data-ttu-id="b4194-109">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span><span class="sxs-lookup"><span data-stu-id="b4194-109">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="b4194-110">This can be done by setting the [TableConnectionPolicy.PreferredLocations](https://docs.microsoft.com/dotnet/api/microsoft.azure.cosmosdb.table.tableconnectionpolicy.preferredlocations?view=azure-dotnet#Microsoft_Azure_CosmosDB_Table_TableConnectionPolicy_PreferredLocations) property.</span><span class="sxs-lookup"><span data-stu-id="b4194-110">This can be done by setting the [TableConnectionPolicy.PreferredLocations](https://docs.microsoft.com/dotnet/api/microsoft.azure.cosmosdb.table.tableconnectionpolicy.preferredlocations?view=azure-dotnet#Microsoft_Azure_CosmosDB_Table_TableConnectionPolicy_PreferredLocations) property.</span></span> <span data-ttu-id="b4194-111">The Azure Cosmos DB Table API SDK picks the best endpoint to communicate with based on the account configuration, current regional availability and the supplied preference list.</span><span class="sxs-lookup"><span data-stu-id="b4194-111">The Azure Cosmos DB Table API SDK picks the best endpoint to communicate with based on the account configuration, current regional availability and the supplied preference list.</span></span>

<span data-ttu-id="b4194-112">The PreferredLocations should contain a comma-separated list of preferred (multi-homing) locations for reads.</span><span class="sxs-lookup"><span data-stu-id="b4194-112">The PreferredLocations should contain a comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="b4194-113">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span><span class="sxs-lookup"><span data-stu-id="b4194-113">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span></span> <span data-ttu-id="b4194-114">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span><span class="sxs-lookup"><span data-stu-id="b4194-114">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span>

<span data-ttu-id="b4194-115">All reads are sent to the first available region in the PreferredLocations list.</span><span class="sxs-lookup"><span data-stu-id="b4194-115">All reads are sent to the first available region in the PreferredLocations list.</span></span> <span data-ttu-id="b4194-116">If the request fails, the client will fail down the list to the next region, and so on.</span><span class="sxs-lookup"><span data-stu-id="b4194-116">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="b4194-117">The SDK attempts to read from the regions specified in PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="b4194-117">The SDK attempts to read from the regions specified in PreferredLocations.</span></span> <span data-ttu-id="b4194-118">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span><span class="sxs-lookup"><span data-stu-id="b4194-118">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="b4194-119">The SDK automatically sends all writes to the current write region.</span><span class="sxs-lookup"><span data-stu-id="b4194-119">The SDK automatically sends all writes to the current write region.</span></span>

<span data-ttu-id="b4194-120">If the PreferredLocations property is not set, all requests will be served from the current write region.</span><span class="sxs-lookup"><span data-stu-id="b4194-120">If the PreferredLocations property is not set, all requests will be served from the current write region.</span></span>

<span data-ttu-id="b4194-121">That's it, that completes this tutorial.</span><span class="sxs-lookup"><span data-stu-id="b4194-121">That's it, that completes this tutorial.</span></span> <span data-ttu-id="b4194-122">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="b4194-122">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="b4194-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="b4194-123">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4194-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="b4194-124">Next steps</span></span>

<span data-ttu-id="b4194-125">In this tutorial, you've done the following:</span><span class="sxs-lookup"><span data-stu-id="b4194-125">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b4194-126">Configure global distribution using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b4194-126">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="b4194-127">Configure global distribution using the Azure Cosmos DB Table APIs</span><span class="sxs-lookup"><span data-stu-id="b4194-127">Configure global distribution using the Azure Cosmos DB Table APIs</span></span>

