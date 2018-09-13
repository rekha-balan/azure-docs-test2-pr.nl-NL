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
ms.openlocfilehash: 37d7b1d44c2a4b2f3cd2fd3ac881b106d5056279
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45109364"
---
<span data-ttu-id="8833d-103">You can now use the Data Explorer tool in the Azure portal to create a database and table.</span><span class="sxs-lookup"><span data-stu-id="8833d-103">You can now use the Data Explorer tool in the Azure portal to create a database and table.</span></span> 

1. <span data-ttu-id="8833d-104">Click **Data Explorer** > **New Table**.</span><span class="sxs-lookup"><span data-stu-id="8833d-104">Click **Data Explorer** > **New Table**.</span></span> 
    
    <span data-ttu-id="8833d-105">The **Add Table** area is displayed on the far right, you may need to scroll right to see it.</span><span class="sxs-lookup"><span data-stu-id="8833d-105">The **Add Table** area is displayed on the far right, you may need to scroll right to see it.</span></span>

    ![Data Explorer in the Azure portal](./media/cosmos-db-create-table/azure-cosmosdb-data-explorer.png)

2. <span data-ttu-id="8833d-107">In the **Add Table** page, enter the settings for the new table.</span><span class="sxs-lookup"><span data-stu-id="8833d-107">In the **Add Table** page, enter the settings for the new table.</span></span>

    <span data-ttu-id="8833d-108">Setting</span><span class="sxs-lookup"><span data-stu-id="8833d-108">Setting</span></span>|<span data-ttu-id="8833d-109">Suggested value</span><span class="sxs-lookup"><span data-stu-id="8833d-109">Suggested value</span></span>|<span data-ttu-id="8833d-110">Description</span><span class="sxs-lookup"><span data-stu-id="8833d-110">Description</span></span>
    ---|---|---
    <span data-ttu-id="8833d-111">Table Id</span><span class="sxs-lookup"><span data-stu-id="8833d-111">Table Id</span></span>|<span data-ttu-id="8833d-112">sample-table</span><span class="sxs-lookup"><span data-stu-id="8833d-112">sample-table</span></span>|<span data-ttu-id="8833d-113">The ID for your new table.</span><span class="sxs-lookup"><span data-stu-id="8833d-113">The ID for your new table.</span></span> <span data-ttu-id="8833d-114">Table names have the same character requirements as database ids.</span><span class="sxs-lookup"><span data-stu-id="8833d-114">Table names have the same character requirements as database ids.</span></span> <span data-ttu-id="8833d-115">Database names must be between 1 and 255 characters, and cannot contain `/ \ # ?` or a trailing space.</span><span class="sxs-lookup"><span data-stu-id="8833d-115">Database names must be between 1 and 255 characters, and cannot contain `/ \ # ?` or a trailing space.</span></span>
    <span data-ttu-id="8833d-116">Storage capacity</span><span class="sxs-lookup"><span data-stu-id="8833d-116">Storage capacity</span></span>| <span data-ttu-id="8833d-117">Fixed (10 GB)</span><span class="sxs-lookup"><span data-stu-id="8833d-117">Fixed (10 GB)</span></span>|<span data-ttu-id="8833d-118">Use the default value of **Fixed (10 GB)**.</span><span class="sxs-lookup"><span data-stu-id="8833d-118">Use the default value of **Fixed (10 GB)**.</span></span> <span data-ttu-id="8833d-119">This value is the storage capacity of the database.</span><span class="sxs-lookup"><span data-stu-id="8833d-119">This value is the storage capacity of the database.</span></span>
    <span data-ttu-id="8833d-120">Throughput</span><span class="sxs-lookup"><span data-stu-id="8833d-120">Throughput</span></span>|<span data-ttu-id="8833d-121">400 RUs</span><span class="sxs-lookup"><span data-stu-id="8833d-121">400 RUs</span></span>|<span data-ttu-id="8833d-122">Change the throughput to 400 request units per second (RU/s).</span><span class="sxs-lookup"><span data-stu-id="8833d-122">Change the throughput to 400 request units per second (RU/s).</span></span> <span data-ttu-id="8833d-123">If you want to reduce latency, you can scale up the throughput later.</span><span class="sxs-lookup"><span data-stu-id="8833d-123">If you want to reduce latency, you can scale up the throughput later.</span></span>

    <span data-ttu-id="8833d-124">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8833d-124">Click **OK**.</span></span>

    <span data-ttu-id="8833d-125">Data Explorer displays the new database and table.</span><span class="sxs-lookup"><span data-stu-id="8833d-125">Data Explorer displays the new database and table.</span></span>

    ![The Azure portal Data Explorer, showing the new database and collection](./media/cosmos-db-create-table/azure-cosmos-db-new-table.png)