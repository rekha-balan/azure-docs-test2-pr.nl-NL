---
title: What to do in the event of an Azure service disruption that affects Azure Key Vault | Microsoft Docs
description: Learn what to do in the event of an Azure service disruption that affects Azure Key Vault.
services: key-vault
documentationcenter: ''
author: adamglick
manager: mbaldwin
editor: ''
ms.assetid: 19a9af63-3032-447b-9d1a-b0125f384edb
ms.service: key-vault
ms.workload: key-vault
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: sumedhb;aglick
ms.openlocfilehash: 6419d54c54e7d19103419262b79e7a5268b2268c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556800"
---
# <a name="azure-key-vault-availability-and-redundancy"></a><span data-ttu-id="dc042-103">Azure Key Vault availability and redundancy</span><span class="sxs-lookup"><span data-stu-id="dc042-103">Azure Key Vault availability and redundancy</span></span>
<span data-ttu-id="dc042-104">Azure Key Vault features multiple layers of redundancy to make sure that your keys and secrets remain available to your application even if individual components of the service fail.</span><span class="sxs-lookup"><span data-stu-id="dc042-104">Azure Key Vault features multiple layers of redundancy to make sure that your keys and secrets remain available to your application even if individual components of the service fail.</span></span>

<span data-ttu-id="dc042-105">The contents of your key vault are replicated within the region and to a secondary region at least 150 miles away but within the same geography.</span><span class="sxs-lookup"><span data-stu-id="dc042-105">The contents of your key vault are replicated within the region and to a secondary region at least 150 miles away but within the same geography.</span></span> <span data-ttu-id="dc042-106">This maintains high durability of your keys and secrets.</span><span class="sxs-lookup"><span data-stu-id="dc042-106">This maintains high durability of your keys and secrets.</span></span> <span data-ttu-id="dc042-107">See the [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span><span class="sxs-lookup"><span data-stu-id="dc042-107">See the [Azure paired regions](https://docs.microsoft.com/en-us/azure/best-practices-availability-paired-regions) document for details on specific region pairs.</span></span>

<span data-ttu-id="dc042-108">If individual components within the key vault service fail, alternate components within the region step in to serve your request to make sure that there is no degradation of functionality.</span><span class="sxs-lookup"><span data-stu-id="dc042-108">If individual components within the key vault service fail, alternate components within the region step in to serve your request to make sure that there is no degradation of functionality.</span></span> <span data-ttu-id="dc042-109">You do not need to take any action to trigger this.</span><span class="sxs-lookup"><span data-stu-id="dc042-109">You do not need to take any action to trigger this.</span></span> <span data-ttu-id="dc042-110">It happens automatically and will be transparent to you.</span><span class="sxs-lookup"><span data-stu-id="dc042-110">It happens automatically and will be transparent to you.</span></span>

<span data-ttu-id="dc042-111">In the rare event that an entire Azure region is unavailable, the requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) to a secondary region.</span><span class="sxs-lookup"><span data-stu-id="dc042-111">In the rare event that an entire Azure region is unavailable, the requests that you make of Azure Key Vault in that region are automatically routed (*failed over*) to a secondary region.</span></span> <span data-ttu-id="dc042-112">When the primary region is available again, requests are routed back (*failed back*) to the primary region.</span><span class="sxs-lookup"><span data-stu-id="dc042-112">When the primary region is available again, requests are routed back (*failed back*) to the primary region.</span></span> <span data-ttu-id="dc042-113">Again, you do not need to take any action because this happens automatically.</span><span class="sxs-lookup"><span data-stu-id="dc042-113">Again, you do not need to take any action because this happens automatically.</span></span>

<span data-ttu-id="dc042-114">There are a few caveats to be aware of:</span><span class="sxs-lookup"><span data-stu-id="dc042-114">There are a few caveats to be aware of:</span></span>

* <span data-ttu-id="dc042-115">In the event of a region failover, it may take a few minutes for the service to fail over.</span><span class="sxs-lookup"><span data-stu-id="dc042-115">In the event of a region failover, it may take a few minutes for the service to fail over.</span></span> <span data-ttu-id="dc042-116">Requests that are made during this time may fail until the failover completes.</span><span class="sxs-lookup"><span data-stu-id="dc042-116">Requests that are made during this time may fail until the failover completes.</span></span>
* <span data-ttu-id="dc042-117">After a failover is complete, your key vault is in read-only mode.</span><span class="sxs-lookup"><span data-stu-id="dc042-117">After a failover is complete, your key vault is in read-only mode.</span></span> <span data-ttu-id="dc042-118">Requests that are supported in this mode are:</span><span class="sxs-lookup"><span data-stu-id="dc042-118">Requests that are supported in this mode are:</span></span>
  * <span data-ttu-id="dc042-119">List key vaults</span><span class="sxs-lookup"><span data-stu-id="dc042-119">List key vaults</span></span>
  * <span data-ttu-id="dc042-120">Get properties of key vaults</span><span class="sxs-lookup"><span data-stu-id="dc042-120">Get properties of key vaults</span></span>
  * <span data-ttu-id="dc042-121">List secrets</span><span class="sxs-lookup"><span data-stu-id="dc042-121">List secrets</span></span>
  * <span data-ttu-id="dc042-122">Get secrets</span><span class="sxs-lookup"><span data-stu-id="dc042-122">Get secrets</span></span>
  * <span data-ttu-id="dc042-123">List keys</span><span class="sxs-lookup"><span data-stu-id="dc042-123">List keys</span></span>
  * <span data-ttu-id="dc042-124">Get (properties of) keys</span><span class="sxs-lookup"><span data-stu-id="dc042-124">Get (properties of) keys</span></span>
  * <span data-ttu-id="dc042-125">Encrypt</span><span class="sxs-lookup"><span data-stu-id="dc042-125">Encrypt</span></span>
  * <span data-ttu-id="dc042-126">Decrypt</span><span class="sxs-lookup"><span data-stu-id="dc042-126">Decrypt</span></span>
  * <span data-ttu-id="dc042-127">Wrap</span><span class="sxs-lookup"><span data-stu-id="dc042-127">Wrap</span></span>
  * <span data-ttu-id="dc042-128">Unwrap</span><span class="sxs-lookup"><span data-stu-id="dc042-128">Unwrap</span></span>
  * <span data-ttu-id="dc042-129">Verify</span><span class="sxs-lookup"><span data-stu-id="dc042-129">Verify</span></span>
  * <span data-ttu-id="dc042-130">Sign</span><span class="sxs-lookup"><span data-stu-id="dc042-130">Sign</span></span>
  * <span data-ttu-id="dc042-131">Backup</span><span class="sxs-lookup"><span data-stu-id="dc042-131">Backup</span></span>
* <span data-ttu-id="dc042-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span><span class="sxs-lookup"><span data-stu-id="dc042-132">After a failover is failed back, all request types (including read *and* write requests) are available.</span></span>

