---
title: Guide to creating a solution template for the  Marketplace | Microsoft Docs
description: Detailed instructions of how to create, certify and deploy a Multi-VM Image Solution Template for purchase on the Azure Marketplace.
services: marketplace-publishing
documentationcenter: ''
author: HannibalSII
manager: hascipio
editor: ''
ms.assetid: e14e05f2-2385-4ce0-b351-0747cb74ba19
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: 644879d285ee8586253c76a7422db18d4adbb5df
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549549"
---
# <a name="guide-to-create-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="70d99-103">Guide to create a solution template for Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="70d99-103">Guide to create a solution template for Azure Marketplace</span></span>
<span data-ttu-id="70d99-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on the creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="70d99-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on the creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="70d99-105">Now we will walk you through the steps for creating a solution template for multiple VMs on the [Publishing Portal][link-pubportal] for the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="70d99-105">Now we will walk you through the steps for creating a solution template for multiple VMs on the [Publishing Portal][link-pubportal] for the Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-the-publishing-portal"></a><span data-ttu-id="70d99-106">Create your solution template offer in the Publishing Portal</span><span class="sxs-lookup"><span data-stu-id="70d99-106">Create your solution template offer in the Publishing Portal</span></span>
<span data-ttu-id="70d99-107">Go to  [https://publish.windowsazure.com](http://publish.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="70d99-107">Go to  [https://publish.windowsazure.com](http://publish.windowsazure.com).</span></span> <span data-ttu-id="70d99-108">When signing in for the first time to the [Publishing Portal](https://publish.windowsazure.com/), use the same account with which your company’s seller profile was registered.</span><span class="sxs-lookup"><span data-stu-id="70d99-108">When signing in for the first time to the [Publishing Portal](https://publish.windowsazure.com/), use the same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="70d99-109">Later, you can add any employee of your company as a co-admin in the Publishing Portal.</span><span class="sxs-lookup"><span data-stu-id="70d99-109">Later, you can add any employee of your company as a co-admin in the Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="70d99-110">1. Select "Solution templates"</span><span class="sxs-lookup"><span data-stu-id="70d99-110">1. Select "Solution templates"</span></span>
  ![drawing][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="70d99-112">2. Create a new solution template</span><span class="sxs-lookup"><span data-stu-id="70d99-112">2. Create a new solution template</span></span>
  ![drawing][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="70d99-114">3. Start with topologies</span><span class="sxs-lookup"><span data-stu-id="70d99-114">3. Start with topologies</span></span>
<span data-ttu-id="70d99-115">A solution template is a "parent" to all of its topologies.</span><span class="sxs-lookup"><span data-stu-id="70d99-115">A solution template is a "parent" to all of its topologies.</span></span> <span data-ttu-id="70d99-116">You can define multiple topologies in one offer/solution template.</span><span class="sxs-lookup"><span data-stu-id="70d99-116">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="70d99-117">When an offer is pushed to staging, it is pushed with all of its topologies.</span><span class="sxs-lookup"><span data-stu-id="70d99-117">When an offer is pushed to staging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="70d99-118">Follow the steps below to define your offer:</span><span class="sxs-lookup"><span data-stu-id="70d99-118">Follow the steps below to define your offer:</span></span>     

* <span data-ttu-id="70d99-119">Create a Topology: “Topology Identifier” is typically the name of the topology for the solution template.</span><span class="sxs-lookup"><span data-stu-id="70d99-119">Create a Topology: “Topology Identifier” is typically the name of the topology for the solution template.</span></span> <span data-ttu-id="70d99-120">The topology identifier is used in the URL as shown below:</span><span class="sxs-lookup"><span data-stu-id="70d99-120">The topology identifier is used in the URL as shown below:</span></span>

  <span data-ttu-id="70d99-121">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="70d99-121">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="70d99-122">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="70d99-122">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="70d99-123">Add a new version.</span><span class="sxs-lookup"><span data-stu-id="70d99-123">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="70d99-124">4. Get your topology versions certified</span><span class="sxs-lookup"><span data-stu-id="70d99-124">4. Get your topology versions certified</span></span>
<span data-ttu-id="70d99-125">Upload a zip file that contains all required files to provision that particular version of the topology.</span><span class="sxs-lookup"><span data-stu-id="70d99-125">Upload a zip file that contains all required files to provision that particular version of the topology.</span></span> <span data-ttu-id="70d99-126">This zip file must contain the following:</span><span class="sxs-lookup"><span data-stu-id="70d99-126">This zip file must contain the following:</span></span>

* <span data-ttu-id="70d99-127">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span><span class="sxs-lookup"><span data-stu-id="70d99-127">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="70d99-128">Any linked templates and all required scripts.</span><span class="sxs-lookup"><span data-stu-id="70d99-128">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="70d99-129">While your developers work on creating the solution template topologies and getting them certified, the business, marketing, and/or legal departments of your company can work on the marketing and legal content.</span><span class="sxs-lookup"><span data-stu-id="70d99-129">While your developers work on creating the solution template topologies and getting them certified, the business, marketing, and/or legal departments of your company can work on the marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="70d99-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="70d99-130">Next steps</span></span>
<span data-ttu-id="70d99-131">Now that you created your solution template and uploaded the zip file, please follow the instructions in the [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing the offer to staging.</span><span class="sxs-lookup"><span data-stu-id="70d99-131">Now that you created your solution template and uploaded the zip file, please follow the instructions in the [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing the offer to staging.</span></span> <span data-ttu-id="70d99-132">To see the full set of marketplace publishing articles, visit [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="70d99-132">To see the full set of marketplace publishing articles, visit [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="70d99-133">You might also be interested in these related articles:</span><span class="sxs-lookup"><span data-stu-id="70d99-133">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="70d99-134">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="70d99-134">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="70d99-135">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="70d99-135">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="70d99-136">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="70d99-136">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="70d99-137">Storage account throttles: [How to Monitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="70d99-137">Storage account throttles: [How to Monitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-publishing/media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com


