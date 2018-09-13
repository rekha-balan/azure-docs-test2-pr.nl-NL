---
title: Azure Cosmos DB Table API for Python | Microsoft Docs
description: Learn all about the Azure Cosmos DB Table API including release dates, retirement dates, and changes made between each version.
services: cosmos-db
author: SnehaGunda
manager: kfile
editor: ''
ms.service: cosmos-db
ms.component: cosmosdb-table
ms.devlang: python
ms.topic: reference
ms.date: 11/20/2017
ms.author: sngun
ms.custom: ''
ms.openlocfilehash: 9d55394f273069cd3497cde334814b91a7123de8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856143"
---
# <a name="azure-cosmos-db-table-api-sdk-for-python-release-notes-and-resources"></a><span data-ttu-id="1e01e-103">Azure Cosmos DB Table API SDK for Python: Release notes and resources</span><span class="sxs-lookup"><span data-stu-id="1e01e-103">Azure Cosmos DB Table API SDK for Python: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [.NET](table-sdk-dotnet.md)
> * [Java](table-sdk-java.md)
> * [Node.js](table-sdk-nodejs.md)
> * [Python](table-sdk-python.md)
 

|   |   |
|---|---|
|<span data-ttu-id="1e01e-108">**SDK download**</span><span class="sxs-lookup"><span data-stu-id="1e01e-108">**SDK download**</span></span>|[<span data-ttu-id="1e01e-109">PyPI</span><span class="sxs-lookup"><span data-stu-id="1e01e-109">PyPI</span></span>](https://pypi.python.org/pypi/azure-cosmosdb-table/)|
|<span data-ttu-id="1e01e-110">**API documentation**</span><span class="sxs-lookup"><span data-stu-id="1e01e-110">**API documentation**</span></span>|[<span data-ttu-id="1e01e-111">Python API reference documentation</span><span class="sxs-lookup"><span data-stu-id="1e01e-111">Python API reference documentation</span></span>](https://azure.github.io/azure-cosmosdb-python/)|
|<span data-ttu-id="1e01e-112">**SDK installation instructions**</span><span class="sxs-lookup"><span data-stu-id="1e01e-112">**SDK installation instructions**</span></span>|[<span data-ttu-id="1e01e-113">Python SDK installation instructions</span><span class="sxs-lookup"><span data-stu-id="1e01e-113">Python SDK installation instructions</span></span>](https://github.com/Azure/azure-cosmosdb-python/tree/master/azure-cosmosdb-table)|
|<span data-ttu-id="1e01e-114">**Contribute to SDK**</span><span class="sxs-lookup"><span data-stu-id="1e01e-114">**Contribute to SDK**</span></span>|[<span data-ttu-id="1e01e-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="1e01e-115">GitHub</span></span>](https://github.com/Azure/azure-cosmosdb-python/tree/master/azure-cosmosdb-table)|
|<span data-ttu-id="1e01e-116">**Current supported platform**</span><span class="sxs-lookup"><span data-stu-id="1e01e-116">**Current supported platform**</span></span>|<span data-ttu-id="1e01e-117">[Python 2.7](https://www.python.org/downloads/) or [Python 3.3, 3.4, 3.5, or 3.6] (https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="1e01e-117">[Python 2.7](https://www.python.org/downloads/) or [Python 3.3, 3.4, 3.5, or 3.6] (https://www.python.org/downloads/)</span></span>|

> [!IMPORTANT]
> If you created a Table API account during the preview, please create a [new Table API account](create-table-dotnet.md#create-a-database-account) to work with the generally available Table API SDKs.
>

## <a name="release-notes"></a><span data-ttu-id="1e01e-119">Release notes</span><span class="sxs-lookup"><span data-stu-id="1e01e-119">Release notes</span></span>

### <a name="a-name100100"></a><span data-ttu-id="1e01e-120"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="1e01e-120"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="1e01e-121">General availability release</span><span class="sxs-lookup"><span data-stu-id="1e01e-121">General availability release</span></span>

### <a name="a-name03710371"></a><span data-ttu-id="1e01e-122"><a name="0.37.1"/>0.37.1</span><span class="sxs-lookup"><span data-stu-id="1e01e-122"><a name="0.37.1"/>0.37.1</span></span>
* <span data-ttu-id="1e01e-123">Pre-release SDK</span><span class="sxs-lookup"><span data-stu-id="1e01e-123">Pre-release SDK</span></span>

## <a name="release-and-retirement-dates"></a><span data-ttu-id="1e01e-124">Release and retirement dates</span><span class="sxs-lookup"><span data-stu-id="1e01e-124">Release and retirement dates</span></span>
<span data-ttu-id="1e01e-125">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span><span class="sxs-lookup"><span data-stu-id="1e01e-125">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="1e01e-126">New features and functionality and optimizations are only added to the current SDK, as such it is  recommended that you always upgrade to the latest SDK version as early as possible.</span><span class="sxs-lookup"><span data-stu-id="1e01e-126">New features and functionality and optimizations are only added to the current SDK, as such it is  recommended that you always upgrade to the latest SDK version as early as possible.</span></span> 

<br/>

| <span data-ttu-id="1e01e-127">Version</span><span class="sxs-lookup"><span data-stu-id="1e01e-127">Version</span></span> | <span data-ttu-id="1e01e-128">Release Date</span><span class="sxs-lookup"><span data-stu-id="1e01e-128">Release Date</span></span> | <span data-ttu-id="1e01e-129">Retirement Date</span><span class="sxs-lookup"><span data-stu-id="1e01e-129">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="1e01e-130">1.0.0</span><span class="sxs-lookup"><span data-stu-id="1e01e-130">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="1e01e-131">November 15, 2017</span><span class="sxs-lookup"><span data-stu-id="1e01e-131">November 15, 2017</span></span> |--- |
| [<span data-ttu-id="1e01e-132">0.37.1</span><span class="sxs-lookup"><span data-stu-id="1e01e-132">0.37.1</span></span>](#0.37.1) |<span data-ttu-id="1e01e-133">October 05, 2017</span><span class="sxs-lookup"><span data-stu-id="1e01e-133">October 05, 2017</span></span> |--- |


## <a name="faq"></a><span data-ttu-id="1e01e-134">FAQ</span><span class="sxs-lookup"><span data-stu-id="1e01e-134">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="1e01e-135">See also</span><span class="sxs-lookup"><span data-stu-id="1e01e-135">See also</span></span>
<span data-ttu-id="1e01e-136">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span><span class="sxs-lookup"><span data-stu-id="1e01e-136">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

