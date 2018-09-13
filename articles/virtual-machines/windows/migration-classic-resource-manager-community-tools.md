---
title: Community tools - Move classic resources to Azure Resource Manager | Microsoft Docs
description: This article catalogs the tools that have been provided by the community to help migrate IaaS resources from classic to the Azure Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: singhkays
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 228b697b-3950-49f5-84bb-283bb56621b1
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 22bf0402c16745dac1c8287b0ceb3598ea41305b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550105"
---
# <a name="community-tools-to-migrate-iaas-resources-from-classic-to-azure-resource-manager"></a><span data-ttu-id="1b87b-103">Community tools to migrate IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b87b-103">Community tools to migrate IaaS resources from classic to Azure Resource Manager</span></span>
<span data-ttu-id="1b87b-104">This article catalogs the tools that have been provided by the community to assist with migration of IaaS resources from classic to the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="1b87b-104">This article catalogs the tools that have been provided by the community to assist with migration of IaaS resources from classic to the Azure Resource Manager deployment model.</span></span>

> [!NOTE]
> <span data-ttu-id="1b87b-105">These tools are not officially supported by Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="1b87b-105">These tools are not officially supported by Microsoft Support.</span></span> <span data-ttu-id="1b87b-106">Therefore they are open sourced on GitHub and we're happy to accept PRs for fixes or additional scenarios.</span><span class="sxs-lookup"><span data-stu-id="1b87b-106">Therefore they are open sourced on GitHub and we're happy to accept PRs for fixes or additional scenarios.</span></span> <span data-ttu-id="1b87b-107">To report an issue, use the GitHub issues feature.</span><span class="sxs-lookup"><span data-stu-id="1b87b-107">To report an issue, use the GitHub issues feature.</span></span>
> 
> <span data-ttu-id="1b87b-108">Migrating with these tools will cause downtime for your classic Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="1b87b-108">Migrating with these tools will cause downtime for your classic Virtual Machine.</span></span> <span data-ttu-id="1b87b-109">If you're looking for platform supported migration, visit</span><span class="sxs-lookup"><span data-stu-id="1b87b-109">If you're looking for platform supported migration, visit</span></span> 
> 
>   * [<span data-ttu-id="1b87b-110">Platform supported migration of IaaS resources from Classic to Azure Resource Manager stack</span><span class="sxs-lookup"><span data-stu-id="1b87b-110">Platform supported migration of IaaS resources from Classic to Azure Resource Manager stack</span></span>](migration-classic-resource-manager-overview.md)
>   * [<span data-ttu-id="1b87b-111">Technical Deep Dive on Platform supported migration from Classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b87b-111">Technical Deep Dive on Platform supported migration from Classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md)
>   * [<span data-ttu-id="1b87b-112">Migrate IaaS resources from Classic to Azure Resource Manager using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b87b-112">Migrate IaaS resources from Classic to Azure Resource Manager using Azure PowerShell</span></span>](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a><span data-ttu-id="1b87b-113">AsmMetadataParser</span><span class="sxs-lookup"><span data-stu-id="1b87b-113">AsmMetadataParser</span></span>
<span data-ttu-id="1b87b-114">This is a collection of helper tools created as part of enterprise migrations from Azure Service Management to Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1b87b-114">This is a collection of helper tools created as part of enterprise migrations from Azure Service Management to Azure Resource Manager.</span></span> <span data-ttu-id="1b87b-115">This tool allows you to replicate your infrastructure into another subscription which can be used for testing migration and iron out any issues before running the migration on your Production subscription.</span><span class="sxs-lookup"><span data-stu-id="1b87b-115">This tool allows you to replicate your infrastructure into another subscription which can be used for testing migration and iron out any issues before running the migration on your Production subscription.</span></span>

[<span data-ttu-id="1b87b-116">Link to the tool documentation</span><span class="sxs-lookup"><span data-stu-id="1b87b-116">Link to the tool documentation</span></span>](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a><span data-ttu-id="1b87b-117">migAz</span><span class="sxs-lookup"><span data-stu-id="1b87b-117">migAz</span></span>
<span data-ttu-id="1b87b-118">migAz is an additional option to migrate a complete set of classic IaaS resources to Azure Resource Manager IaaS resources.</span><span class="sxs-lookup"><span data-stu-id="1b87b-118">migAz is an additional option to migrate a complete set of classic IaaS resources to Azure Resource Manager IaaS resources.</span></span> <span data-ttu-id="1b87b-119">The migration can occur within the same subscription or between different subscriptions and subscription types (ex: CSP subscriptions).</span><span class="sxs-lookup"><span data-stu-id="1b87b-119">The migration can occur within the same subscription or between different subscriptions and subscription types (ex: CSP subscriptions).</span></span>

[<span data-ttu-id="1b87b-120">Link to the tool documentation</span><span class="sxs-lookup"><span data-stu-id="1b87b-120">Link to the tool documentation</span></span>](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/migaz)

## <a name="next-steps"></a><span data-ttu-id="1b87b-121">Next Steps</span><span class="sxs-lookup"><span data-stu-id="1b87b-121">Next Steps</span></span>

* [<span data-ttu-id="1b87b-122">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b87b-122">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="1b87b-123">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b87b-123">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="1b87b-124">Planning for migration of IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b87b-124">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="1b87b-125">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b87b-125">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="1b87b-126">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b87b-126">Use CLI to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="1b87b-127">Review most common migration errors</span><span class="sxs-lookup"><span data-stu-id="1b87b-127">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="1b87b-128">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b87b-128">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

