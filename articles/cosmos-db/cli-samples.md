---
title: Azure CLI Samples for Azure Cosmos DB | Microsoft Docs
description: Azure CLI Samples - Create and manage Azure Cosmos DB accounts, databases, containers, regions, and firewalls.
services: cosmos-db
author: SnehaGunda
manager: kfile
tags: azure-service-management
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.date: 11/29/2017
ms.author: sngun
ms.openlocfilehash: 42cfe71210b95732b4b69f7ca21a8b647e187a38
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968979"
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a><span data-ttu-id="f8070-103">Azure CLI samples for Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f8070-103">Azure CLI samples for Azure Cosmos DB</span></span>

<span data-ttu-id="f8070-104">The following table includes links to sample Azure CLI scripts for Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f8070-104">The following table includes links to sample Azure CLI scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="f8070-105">Reference pages for all Azure Cosmos DB CLI commands are available in the [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span><span class="sxs-lookup"><span data-stu-id="f8070-105">Reference pages for all Azure Cosmos DB CLI commands are available in the [Azure CLI 2.0 Reference](https://docs.microsoft.com/cli/azure/cosmosdb).</span></span>

| |  |
|---|---|
|<span data-ttu-id="f8070-106">**Create Azure Cosmos DB account, database, and containers**</span><span class="sxs-lookup"><span data-stu-id="f8070-106">**Create Azure Cosmos DB account, database, and containers**</span></span>||
|[<span data-ttu-id="f8070-107">Create a SQL API account</span><span class="sxs-lookup"><span data-stu-id="f8070-107">Create a SQL API account</span></span>](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="f8070-108">Creates a single Azure Cosmos DB API account, database, and container for use with the SQL API.</span><span class="sxs-lookup"><span data-stu-id="f8070-108">Creates a single Azure Cosmos DB API account, database, and container for use with the SQL API.</span></span> |
| [<span data-ttu-id="f8070-109">Create a MongoDB API account</span><span class="sxs-lookup"><span data-stu-id="f8070-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="f8070-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span><span class="sxs-lookup"><span data-stu-id="f8070-110">Creates a single Azure Cosmos DB MongoDB API account, database, and collection.</span></span> |
| [<span data-ttu-id="f8070-111">Create a Gremlin API account</span><span class="sxs-lookup"><span data-stu-id="f8070-111">Create a Gremlin API account</span></span>](scripts/create-graph-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="f8070-112">Creates a single Azure Cosmos DB Gremlin API account, database, and container.</span><span class="sxs-lookup"><span data-stu-id="f8070-112">Creates a single Azure Cosmos DB Gremlin API account, database, and container.</span></span> |
|<span data-ttu-id="f8070-113">**Scale Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="f8070-113">**Scale Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="f8070-114">Scale container throughput</span><span class="sxs-lookup"><span data-stu-id="f8070-114">Scale container throughput</span></span>](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="f8070-115">Changes the provisioned throughput on a container.</span><span class="sxs-lookup"><span data-stu-id="f8070-115">Changes the provisioned throughput on a container.</span></span>|
|[<span data-ttu-id="f8070-116">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span><span class="sxs-lookup"><span data-stu-id="f8070-116">Replicate Azure Cosmos DB database account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="f8070-117">Globally replicates account data into multiple regions with a specified failover priority.</span><span class="sxs-lookup"><span data-stu-id="f8070-117">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="f8070-118">**Secure Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="f8070-118">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="f8070-119">Get account keys</span><span class="sxs-lookup"><span data-stu-id="f8070-119">Get account keys</span></span>](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="f8070-120">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span><span class="sxs-lookup"><span data-stu-id="f8070-120">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span></span>|
| [<span data-ttu-id="f8070-121">Get MongoDB connection string</span><span class="sxs-lookup"><span data-stu-id="f8070-121">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | <span data-ttu-id="f8070-122">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="f8070-122">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="f8070-123">Regenerate account keys</span><span class="sxs-lookup"><span data-stu-id="f8070-123">Regenerate account keys</span></span>](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="f8070-124">Regenerates the master or read-only key for the account.</span><span class="sxs-lookup"><span data-stu-id="f8070-124">Regenerates the master or read-only key for the account.</span></span>|
|[<span data-ttu-id="f8070-125">Create a firewall</span><span class="sxs-lookup"><span data-stu-id="f8070-125">Create a firewall</span></span>](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| <span data-ttu-id="f8070-126">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span><span class="sxs-lookup"><span data-stu-id="f8070-126">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="f8070-127">**High availability, disaster recovery, backup and restore**</span><span class="sxs-lookup"><span data-stu-id="f8070-127">**High availability, disaster recovery, backup and restore**</span></span>||
|[<span data-ttu-id="f8070-128">Configure failover policy</span><span class="sxs-lookup"><span data-stu-id="f8070-128">Configure failover policy</span></span>](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="f8070-129">Sets the failover priority of each region in which the account is replicated.</span><span class="sxs-lookup"><span data-stu-id="f8070-129">Sets the failover priority of each region in which the account is replicated.</span></span>|
|<span data-ttu-id="f8070-130">**Connect Azure Cosmos DB to resources**</span><span class="sxs-lookup"><span data-stu-id="f8070-130">**Connect Azure Cosmos DB to resources**</span></span>||
|[<span data-ttu-id="f8070-131">Connect a web app to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f8070-131">Connect a web app to Azure Cosmos DB</span></span>](../app-service/scripts/app-service-cli-app-service-documentdb.md?toc=%2fcli%2fazure%2ftoc.json)|<span data-ttu-id="f8070-132">Create and connect an Azure Cosmos DB database and an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="f8070-132">Create and connect an Azure Cosmos DB database and an Azure web app.</span></span>|
|||
