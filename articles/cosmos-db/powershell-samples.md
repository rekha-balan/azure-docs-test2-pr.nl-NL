---
title: Azure PowerShell Samples for Azure Cosmos DB | Microsoft Docs
description: Azure PowerShell Samples - Scripts to help you create and manage Azure Cosmos DB accounts.
services: cosmos-db
author: SnehaGunda
manager: kfile
tags: azure-service-management
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: na
ms.topic: sample
ms.date: 10/16/2017
ms.author: sngun
ms.openlocfilehash: 9ee5c7a008f375beffd6bbdf00cca8b28752b1fb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865834"
---
# <a name="azure-powershell-samples-for-azure-cosmos-db"></a><span data-ttu-id="84779-103">Azure PowerShell samples for Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="84779-103">Azure PowerShell samples for Azure Cosmos DB</span></span>

<span data-ttu-id="84779-104">The following table includes links to sample Azure PowerShell scripts for Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="84779-104">The following table includes links to sample Azure PowerShell scripts for Azure Cosmos DB.</span></span> <span data-ttu-id="84779-105">At this time, you can only manage the Azure Cosmos DB account via PowerShell; other resources such as databases and containers cannot be managed via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84779-105">At this time, you can only manage the Azure Cosmos DB account via PowerShell; other resources such as databases and containers cannot be managed via PowerShell.</span></span>

| |  |
|---|---|
|<span data-ttu-id="84779-106">**Create an Azure Cosmos DB account**</span><span class="sxs-lookup"><span data-stu-id="84779-106">**Create an Azure Cosmos DB account**</span></span>||
|[<span data-ttu-id="84779-107">Create a SQL API account</span><span class="sxs-lookup"><span data-stu-id="84779-107">Create a SQL API account</span></span>](scripts/create-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="84779-108">Creates a single Azure Cosmos DB account to use with the SQL API.</span><span class="sxs-lookup"><span data-stu-id="84779-108">Creates a single Azure Cosmos DB account to use with the SQL API.</span></span> |
|[<span data-ttu-id="84779-109">Create a MongoDB API account</span><span class="sxs-lookup"><span data-stu-id="84779-109">Create a MongoDB API account</span></span>](scripts/create-mongodb-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="84779-110">Creates a single Azure Cosmos DB account to use with the MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="84779-110">Creates a single Azure Cosmos DB account to use with the MongoDB API.</span></span> |
|[<span data-ttu-id="84779-111">Create a Gremlin API account</span><span class="sxs-lookup"><span data-stu-id="84779-111">Create a Gremlin API account</span></span>](scripts/create-graph-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="84779-112">Creates a single Azure Cosmos DB account to use with the Gremlin API.</span><span class="sxs-lookup"><span data-stu-id="84779-112">Creates a single Azure Cosmos DB account to use with the Gremlin API.</span></span> |
|[<span data-ttu-id="84779-113">Create a Cassandra API account</span><span class="sxs-lookup"><span data-stu-id="84779-113">Create a Cassandra API account</span></span>](scripts/create-and-configure-cassandra-database.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="84779-114">Creates a single Azure Cosmos DB account to use with the Cassandra API.</span><span class="sxs-lookup"><span data-stu-id="84779-114">Creates a single Azure Cosmos DB account to use with the Cassandra API.</span></span> |
|[<span data-ttu-id="84779-115">Create a Table API account</span><span class="sxs-lookup"><span data-stu-id="84779-115">Create a Table API account</span></span>](scripts/create-table-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="84779-116">Creates a single Azure Cosmos DB account to use with the Table API.</span><span class="sxs-lookup"><span data-stu-id="84779-116">Creates a single Azure Cosmos DB account to use with the Table API.</span></span> |
|<span data-ttu-id="84779-117">**Scale Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="84779-117">**Scale Azure Cosmos DB**</span></span>||
|[<span data-ttu-id="84779-118">Replicate Azure Cosmos DB account in multiple regions and configure failover priorities</span><span class="sxs-lookup"><span data-stu-id="84779-118">Replicate Azure Cosmos DB account in multiple regions and configure failover priorities</span></span>](scripts/scale-multiregion-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="84779-119">Globally replicates account data into multiple regions with a specified failover priority.</span><span class="sxs-lookup"><span data-stu-id="84779-119">Globally replicates account data into multiple regions with a specified failover priority.</span></span>|
|<span data-ttu-id="84779-120">**Secure Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="84779-120">**Secure Azure Cosmos DB**</span></span>||
| [<span data-ttu-id="84779-121">Get account keys</span><span class="sxs-lookup"><span data-stu-id="84779-121">Get account keys</span></span>](scripts/secure-get-account-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="84779-122">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span><span class="sxs-lookup"><span data-stu-id="84779-122">Gets the primary and secondary master write keys and primary and secondary read-only keys for the account.</span></span>|
| [<span data-ttu-id="84779-123">Get MongoDB connection string</span><span class="sxs-lookup"><span data-stu-id="84779-123">Get MongoDB connection string</span></span>](scripts/secure-mongo-connection-string-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | <span data-ttu-id="84779-124">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="84779-124">Gets the connection string to connect your MongoDB app to your Azure Cosmos DB account.</span></span>|
|[<span data-ttu-id="84779-125">Regenerate account keys</span><span class="sxs-lookup"><span data-stu-id="84779-125">Regenerate account keys</span></span>](scripts/secure-regenerate-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="84779-126">Regenerates the master or read-only key for the account.</span><span class="sxs-lookup"><span data-stu-id="84779-126">Regenerates the master or read-only key for the account.</span></span>|
|[<span data-ttu-id="84779-127">Create a firewall</span><span class="sxs-lookup"><span data-stu-id="84779-127">Create a firewall</span></span>](scripts/create-firewall-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| <span data-ttu-id="84779-128">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span><span class="sxs-lookup"><span data-stu-id="84779-128">Creates an inbound IP access control policy to limit access to the account from an approved set of machines and/or cloud services.</span></span>|
|<span data-ttu-id="84779-129">**High availability, disaster recovery, backup, and restore**</span><span class="sxs-lookup"><span data-stu-id="84779-129">**High availability, disaster recovery, backup, and restore**</span></span>||
|[<span data-ttu-id="84779-130">Configure failover policy</span><span class="sxs-lookup"><span data-stu-id="84779-130">Configure failover policy</span></span>](scripts/ha-failover-policy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|<span data-ttu-id="84779-131">Sets the failover priority of each region in which the account is replicated.</span><span class="sxs-lookup"><span data-stu-id="84779-131">Sets the failover priority of each region in which the account is replicated.</span></span>|
|||
