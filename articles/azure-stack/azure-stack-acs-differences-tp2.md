---
title: 'Azure-consistent storage: differences and considerations | Microsoft Docs'
description: Understand the differences from Azure Storage and other Azure-consistent storage deployment considerations.
services: azure-stack
documentationcenter: ''
author: MChadalapaka
manager: siroy
editor: ''
ms.assetid: 1d720ffa-848d-4853-b7b4-ac726fe82e99
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/26/2016
ms.author: mchad
ms.openlocfilehash: 28a83a899c5c4c261a2b63bf96baf4b040b5585f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564045"
---
# <a name="azure-consistent-storage-differences-and-considerations"></a><span data-ttu-id="cff6a-103">Azure-consistent storage: differences and considerations</span><span class="sxs-lookup"><span data-stu-id="cff6a-103">Azure-consistent storage: differences and considerations</span></span>
<span data-ttu-id="cff6a-104">Azure-consistent storage is the set of storage cloud services in Microsoft Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="cff6a-104">Azure-consistent storage is the set of storage cloud services in Microsoft Azure Stack.</span></span> <span data-ttu-id="cff6a-105">Azure-consistent storage provides blob, table, queue, and account management functionality with Azure-consistent semantics.</span><span class="sxs-lookup"><span data-stu-id="cff6a-105">Azure-consistent storage provides blob, table, queue, and account management functionality with Azure-consistent semantics.</span></span> <span data-ttu-id="cff6a-106">This article summarizes the known Azure-consistent storage differences with Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="cff6a-106">This article summarizes the known Azure-consistent storage differences with Azure Storage.</span></span> <span data-ttu-id="cff6a-107">It also summarizes other considerations to keep in mind when you deploy the currently publicly available preview version of Microsoft Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="cff6a-107">It also summarizes other considerations to keep in mind when you deploy the currently publicly available preview version of Microsoft Azure Stack.</span></span>

<span id="Concepts" class="anchor"><span id="_Toc386544169" class="anchor"><span id="_Toc389466742" class="anchor"><span id="_Ref428966996" class="anchor"><span id="_Toc433223853" class="anchor"></span></span></span></span></span>

## <a name="known-differences"></a><span data-ttu-id="cff6a-108">Known differences</span><span class="sxs-lookup"><span data-stu-id="cff6a-108">Known differences</span></span>
<span data-ttu-id="cff6a-109">This Technical Preview version of Azure-consistent storage does not have 100% feature parity with Azure Storage for the API versions that are supported.</span><span class="sxs-lookup"><span data-stu-id="cff6a-109">This Technical Preview version of Azure-consistent storage does not have 100% feature parity with Azure Storage for the API versions that are supported.</span></span> <span data-ttu-id="cff6a-110">Known feature differences include the following:</span><span class="sxs-lookup"><span data-stu-id="cff6a-110">Known feature differences include the following:</span></span>

* <span data-ttu-id="cff6a-111">Certain storage account types are not yet available, for example, Standard\_RAGRS and Standard\_GRS.</span><span class="sxs-lookup"><span data-stu-id="cff6a-111">Certain storage account types are not yet available, for example, Standard\_RAGRS and Standard\_GRS.</span></span>
* <span data-ttu-id="cff6a-112">Premium\_LRS storage accounts can be provisioned.</span><span class="sxs-lookup"><span data-stu-id="cff6a-112">Premium\_LRS storage accounts can be provisioned.</span></span> <span data-ttu-id="cff6a-113">However, there are currently no performance limits or guarantees.</span><span class="sxs-lookup"><span data-stu-id="cff6a-113">However, there are currently no performance limits or guarantees.</span></span>
* <span data-ttu-id="cff6a-114">Azure Files functionality is not yet available.</span><span class="sxs-lookup"><span data-stu-id="cff6a-114">Azure Files functionality is not yet available.</span></span>
* <span data-ttu-id="cff6a-115">The Get Page Ranges API does not support the retrieval of pages that differ between snapshots of page blobs.</span><span class="sxs-lookup"><span data-stu-id="cff6a-115">The Get Page Ranges API does not support the retrieval of pages that differ between snapshots of page blobs.</span></span>
* <span data-ttu-id="cff6a-116">The Get Page Ranges API returns pages that have 4 KB of granularity.</span><span class="sxs-lookup"><span data-stu-id="cff6a-116">The Get Page Ranges API returns pages that have 4 KB of granularity.</span></span>
* <span data-ttu-id="cff6a-117">Partition Key and Row Key in the Azure-consistent storage Table implementation are each limited to 400 characters (that is, 800 bytes) in size.</span><span class="sxs-lookup"><span data-stu-id="cff6a-117">Partition Key and Row Key in the Azure-consistent storage Table implementation are each limited to 400 characters (that is, 800 bytes) in size.</span></span>
* <span data-ttu-id="cff6a-118">Blob names in the Azure-consistent storage Blob service implementation are limited to 880 characters (that is, 1760 bytes) in size.</span><span class="sxs-lookup"><span data-stu-id="cff6a-118">Blob names in the Azure-consistent storage Blob service implementation are limited to 880 characters (that is, 1760 bytes) in size.</span></span>
* <span data-ttu-id="cff6a-119">The Azure-consistent storage implementation of tenant storage usage data reporting provides storage usage meters that are identical to those in Azure, with the same semantics and units.</span><span class="sxs-lookup"><span data-stu-id="cff6a-119">The Azure-consistent storage implementation of tenant storage usage data reporting provides storage usage meters that are identical to those in Azure, with the same semantics and units.</span></span> <span data-ttu-id="cff6a-120">Currently, however, the Storage Transactions usage meter does not include IaaS transactions, and the Data Transfer usage meter does not differentiate the bandwidth usage by internal or external network traffic to an Azure Stack region.</span><span class="sxs-lookup"><span data-stu-id="cff6a-120">Currently, however, the Storage Transactions usage meter does not include IaaS transactions, and the Data Transfer usage meter does not differentiate the bandwidth usage by internal or external network traffic to an Azure Stack region.</span></span>
* <span data-ttu-id="cff6a-121">Certain differences exist in the scope of functionality for storage manageability.</span><span class="sxs-lookup"><span data-stu-id="cff6a-121">Certain differences exist in the scope of functionality for storage manageability.</span></span> <span data-ttu-id="cff6a-122">For example, you can't change the account type or have custom domains.</span><span class="sxs-lookup"><span data-stu-id="cff6a-122">For example, you can't change the account type or have custom domains.</span></span> <span data-ttu-id="cff6a-123">In addition, only API-level consistency is offered for the Premium\_LRS storage account type.</span><span class="sxs-lookup"><span data-stu-id="cff6a-123">In addition, only API-level consistency is offered for the Premium\_LRS storage account type.</span></span>

## <a name="deployment-considerations"></a><span data-ttu-id="cff6a-124">Deployment considerations</span><span class="sxs-lookup"><span data-stu-id="cff6a-124">Deployment considerations</span></span>
* <span data-ttu-id="cff6a-125">**Test only.**</span><span class="sxs-lookup"><span data-stu-id="cff6a-125">**Test only.**</span></span> <span data-ttu-id="cff6a-126">Do not deploy Azure-consistent storage in production environments that use the current Microsoft Azure Stack Technical Preview release.</span><span class="sxs-lookup"><span data-stu-id="cff6a-126">Do not deploy Azure-consistent storage in production environments that use the current Microsoft Azure Stack Technical Preview release.</span></span> <span data-ttu-id="cff6a-127">This version is meant only for evaluation purposes in a test lab environment.</span><span class="sxs-lookup"><span data-stu-id="cff6a-127">This version is meant only for evaluation purposes in a test lab environment.</span></span>
* <span data-ttu-id="cff6a-128">**Performance**.</span><span class="sxs-lookup"><span data-stu-id="cff6a-128">**Performance**.</span></span> <span data-ttu-id="cff6a-129">The Microsoft Azure Stack Technical Preview version of Azure-consistent storage is not fully performance-optimized.</span><span class="sxs-lookup"><span data-stu-id="cff6a-129">The Microsoft Azure Stack Technical Preview version of Azure-consistent storage is not fully performance-optimized.</span></span>
* <span data-ttu-id="cff6a-130">**Scalability.**</span><span class="sxs-lookup"><span data-stu-id="cff6a-130">**Scalability.**</span></span> <span data-ttu-id="cff6a-131">The Microsoft Azure Stack Technical Preview version of Azure-consistent storage is not optimized for scalability.</span><span class="sxs-lookup"><span data-stu-id="cff6a-131">The Microsoft Azure Stack Technical Preview version of Azure-consistent storage is not optimized for scalability.</span></span>

## <a name="version-support-considerations"></a><span data-ttu-id="cff6a-132">Version support considerations</span><span class="sxs-lookup"><span data-stu-id="cff6a-132">Version support considerations</span></span>
<span data-ttu-id="cff6a-133">The following versions are supported with this preview release of Azure-consistent storage:</span><span class="sxs-lookup"><span data-stu-id="cff6a-133">The following versions are supported with this preview release of Azure-consistent storage:</span></span>

> <span data-ttu-id="cff6a-134">Azure Storage Client Library: [Microsoft Azure Storage 6.x .NET SDK](http://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)</span><span class="sxs-lookup"><span data-stu-id="cff6a-134">Azure Storage Client Library: [Microsoft Azure Storage 6.x .NET SDK](http://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)</span></span>
> 
> <span data-ttu-id="cff6a-135">Azure Storage data services: [2015-04-05 REST API version](https://msdn.microsoft.com/library/azure/mt705637.aspx)</span><span class="sxs-lookup"><span data-stu-id="cff6a-135">Azure Storage data services: [2015-04-05 REST API version](https://msdn.microsoft.com/library/azure/mt705637.aspx)</span></span>
> 
> <span data-ttu-id="cff6a-136">Azure Storage management services: [2015-05-01-preview](https://msdn.microsoft.com/library/azure/mt163683.aspx)
> [2015-06-15](https://msdn.microsoft.com/library/azure/mt163683.aspx)</span><span class="sxs-lookup"><span data-stu-id="cff6a-136">Azure Storage management services: [2015-05-01-preview](https://msdn.microsoft.com/library/azure/mt163683.aspx)
> [2015-06-15](https://msdn.microsoft.com/library/azure/mt163683.aspx)</span></span>
> 
> ## <a name="next-steps"></a><span data-ttu-id="cff6a-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="cff6a-137">Next steps</span></span>
> 

* [<span data-ttu-id="cff6a-138">Introduction to Azure-consistent storage</span><span class="sxs-lookup"><span data-stu-id="cff6a-138">Introduction to Azure-consistent storage</span></span>](azure-stack-storage-overview.md)

