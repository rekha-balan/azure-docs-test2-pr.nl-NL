---
title: include file
description: include file
services: cosmos-db
author: SnehaGunda
ms.service: cosmos-db
ms.topic: include
ms.date: 04/13/2018
ms.author: sngun
ms.custom: include file
ms.openlocfilehash: b656001c8a7d1bed21c208bc643018c5f751e09c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45321642"
---
<span data-ttu-id="852bf-103">You can now use the Data Explorer tool in the Azure portal to create a graph database.</span><span class="sxs-lookup"><span data-stu-id="852bf-103">You can now use the Data Explorer tool in the Azure portal to create a graph database.</span></span> 

1. <span data-ttu-id="852bf-104">Click **Data Explorer** > **New Graph**.</span><span class="sxs-lookup"><span data-stu-id="852bf-104">Click **Data Explorer** > **New Graph**.</span></span>

    <span data-ttu-id="852bf-105">The **Add Graph** area is displayed on the far right, you may need to scroll right to see it.</span><span class="sxs-lookup"><span data-stu-id="852bf-105">The **Add Graph** area is displayed on the far right, you may need to scroll right to see it.</span></span>

    ![The Azure portal Data Explorer, Add Graph page](./media/cosmos-db-create-graph/azure-cosmosdb-data-explorer-graph.png)

2. <span data-ttu-id="852bf-107">In the **Add graph** page, enter the settings for the new graph.</span><span class="sxs-lookup"><span data-stu-id="852bf-107">In the **Add graph** page, enter the settings for the new graph.</span></span>

    <span data-ttu-id="852bf-108">Setting</span><span class="sxs-lookup"><span data-stu-id="852bf-108">Setting</span></span>|<span data-ttu-id="852bf-109">Suggested value</span><span class="sxs-lookup"><span data-stu-id="852bf-109">Suggested value</span></span>|<span data-ttu-id="852bf-110">Description</span><span class="sxs-lookup"><span data-stu-id="852bf-110">Description</span></span>
    ---|---|---
    <span data-ttu-id="852bf-111">Database ID</span><span class="sxs-lookup"><span data-stu-id="852bf-111">Database ID</span></span>|<span data-ttu-id="852bf-112">sample-database</span><span class="sxs-lookup"><span data-stu-id="852bf-112">sample-database</span></span>|<span data-ttu-id="852bf-113">Enter *sample-database* as the name for the new database.</span><span class="sxs-lookup"><span data-stu-id="852bf-113">Enter *sample-database* as the name for the new database.</span></span> <span data-ttu-id="852bf-114">Database names must be between 1 and 255 characters, and cannot contain `/ \ # ?` or a trailing space.</span><span class="sxs-lookup"><span data-stu-id="852bf-114">Database names must be between 1 and 255 characters, and cannot contain `/ \ # ?` or a trailing space.</span></span>
    <span data-ttu-id="852bf-115">Graph ID</span><span class="sxs-lookup"><span data-stu-id="852bf-115">Graph ID</span></span>|<span data-ttu-id="852bf-116">sample-graph</span><span class="sxs-lookup"><span data-stu-id="852bf-116">sample-graph</span></span>|<span data-ttu-id="852bf-117">Enter *sample-graph* as the name for your new collection.</span><span class="sxs-lookup"><span data-stu-id="852bf-117">Enter *sample-graph* as the name for your new collection.</span></span> <span data-ttu-id="852bf-118">Graph names have the same character requirements as database IDs.</span><span class="sxs-lookup"><span data-stu-id="852bf-118">Graph names have the same character requirements as database IDs.</span></span>
    <span data-ttu-id="852bf-119">Storage Capacity</span><span class="sxs-lookup"><span data-stu-id="852bf-119">Storage Capacity</span></span>|<span data-ttu-id="852bf-120">Fixed (10 GB)</span><span class="sxs-lookup"><span data-stu-id="852bf-120">Fixed (10 GB)</span></span>|<span data-ttu-id="852bf-121">Leave the default value of **Fixed (10 GB)**.</span><span class="sxs-lookup"><span data-stu-id="852bf-121">Leave the default value of **Fixed (10 GB)**.</span></span> <span data-ttu-id="852bf-122">This value is the storage capacity of the database.</span><span class="sxs-lookup"><span data-stu-id="852bf-122">This value is the storage capacity of the database.</span></span>
    <span data-ttu-id="852bf-123">Throughput</span><span class="sxs-lookup"><span data-stu-id="852bf-123">Throughput</span></span>|<span data-ttu-id="852bf-124">400 RUs</span><span class="sxs-lookup"><span data-stu-id="852bf-124">400 RUs</span></span>|<span data-ttu-id="852bf-125">Change the throughput to 400 request units per second (RU/s).</span><span class="sxs-lookup"><span data-stu-id="852bf-125">Change the throughput to 400 request units per second (RU/s).</span></span> <span data-ttu-id="852bf-126">If you want to reduce latency, you can scale up the throughput later.</span><span class="sxs-lookup"><span data-stu-id="852bf-126">If you want to reduce latency, you can scale up the throughput later.</span></span>

3. <span data-ttu-id="852bf-127">Once the form is filled out, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="852bf-127">Once the form is filled out, click **OK**.</span></span>
