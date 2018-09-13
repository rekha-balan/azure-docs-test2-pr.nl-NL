---
title: Subscription and account for Linux VMs in Azure | Microsoft Docs
description: Learn about the key design and implementation guidelines for subscriptions and accounts on Azure.
documentationcenter: ''
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 19343826-7eef-42a1-98be-4ec65b0f377a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5e55bab3ee915b05cbcffad217f3db509e88a6c0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549299"
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a><span data-ttu-id="3b2f8-103">Azure subscription and accounts guidelines for Linux VMs</span><span class="sxs-lookup"><span data-stu-id="3b2f8-103">Azure subscription and accounts guidelines for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="3b2f8-104">This article focuses on understanding how to approach subscription and account management as your environment and user base grows.</span><span class="sxs-lookup"><span data-stu-id="3b2f8-104">This article focuses on understanding how to approach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="3b2f8-105">Implementation guidelines for subscriptions and accounts</span><span class="sxs-lookup"><span data-stu-id="3b2f8-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="3b2f8-106">Decisions:</span><span class="sxs-lookup"><span data-stu-id="3b2f8-106">Decisions:</span></span>

* <span data-ttu-id="3b2f8-107">What set of subscriptions and accounts do you need to host your IT workload or infrastructure?</span><span class="sxs-lookup"><span data-stu-id="3b2f8-107">What set of subscriptions and accounts do you need to host your IT workload or infrastructure?</span></span>
* <span data-ttu-id="3b2f8-108">How to break down the hierarchy to fit your organization?</span><span class="sxs-lookup"><span data-stu-id="3b2f8-108">How to break down the hierarchy to fit your organization?</span></span>

<span data-ttu-id="3b2f8-109">Tasks:</span><span class="sxs-lookup"><span data-stu-id="3b2f8-109">Tasks:</span></span>

* <span data-ttu-id="3b2f8-110">Define your logical organization hierarchy as you would like to manage it from a subscription level.</span><span class="sxs-lookup"><span data-stu-id="3b2f8-110">Define your logical organization hierarchy as you would like to manage it from a subscription level.</span></span>
* <span data-ttu-id="3b2f8-111">To match this logical hierarchy, define the accounts required and subscriptions under each account.</span><span class="sxs-lookup"><span data-stu-id="3b2f8-111">To match this logical hierarchy, define the accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="3b2f8-112">Create the set of subscriptions and accounts using your naming convention.</span><span class="sxs-lookup"><span data-stu-id="3b2f8-112">Create the set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="3b2f8-113">Subscriptions and accounts</span><span class="sxs-lookup"><span data-stu-id="3b2f8-113">Subscriptions and accounts</span></span>
<span data-ttu-id="3b2f8-114">To work with Azure, you need one or more Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="3b2f8-114">To work with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="3b2f8-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span><span class="sxs-lookup"><span data-stu-id="3b2f8-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="3b2f8-116">Enterprise customers typically have an Enterprise Enrollment, which is the top-most resource in the hierarchy, and is associated to one or more accounts.</span><span class="sxs-lookup"><span data-stu-id="3b2f8-116">Enterprise customers typically have an Enterprise Enrollment, which is the top-most resource in the hierarchy, and is associated to one or more accounts.</span></span>
* <span data-ttu-id="3b2f8-117">For consumers and customers without an Enterprise Enrollment, the top-most resource is the account.</span><span class="sxs-lookup"><span data-stu-id="3b2f8-117">For consumers and customers without an Enterprise Enrollment, the top-most resource is the account.</span></span>
* <span data-ttu-id="3b2f8-118">Subscriptions are associated to accounts, and there can be one or more subscriptions per account.</span><span class="sxs-lookup"><span data-stu-id="3b2f8-118">Subscriptions are associated to accounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="3b2f8-119">Azure records billing information at the subscription level.</span><span class="sxs-lookup"><span data-stu-id="3b2f8-119">Azure records billing information at the subscription level.</span></span>

<span data-ttu-id="3b2f8-120">Due to the limit of two hierarchy levels on the Account/Subscription relationship, it is important to align the naming convention of accounts and subscriptions to the billing needs.</span><span class="sxs-lookup"><span data-stu-id="3b2f8-120">Due to the limit of two hierarchy levels on the Account/Subscription relationship, it is important to align the naming convention of accounts and subscriptions to the billing needs.</span></span> <span data-ttu-id="3b2f8-121">For instance, if a global company uses Azure, they might choose to have one account per region, and have subscriptions managed at the region level:</span><span class="sxs-lookup"><span data-stu-id="3b2f8-121">For instance, if a global company uses Azure, they might choose to have one account per region, and have subscriptions managed at the region level:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="3b2f8-122">For instance, you might use the following structure:</span><span class="sxs-lookup"><span data-stu-id="3b2f8-122">For instance, you might use the following structure:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="3b2f8-123">If a region decides to have more than one subscription associated to a particular group, the naming convention should incorporate a way to encode the extra data on either the account or the subscription name.</span><span class="sxs-lookup"><span data-stu-id="3b2f8-123">If a region decides to have more than one subscription associated to a particular group, the naming convention should incorporate a way to encode the extra data on either the account or the subscription name.</span></span> <span data-ttu-id="3b2f8-124">This organization allows massaging billing data to generate the new levels of hierarchy during billing reports:</span><span class="sxs-lookup"><span data-stu-id="3b2f8-124">This organization allows massaging billing data to generate the new levels of hierarchy during billing reports:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="3b2f8-125">The organization could look like the following example:</span><span class="sxs-lookup"><span data-stu-id="3b2f8-125">The organization could look like the following example:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="3b2f8-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span><span class="sxs-lookup"><span data-stu-id="3b2f8-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b2f8-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="3b2f8-127">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]





