---
title: Publish a custom marketplace item in Azure Stack (service administrator) | Microsoft Docs
description: As a service administrator, learn how to publish a custom marketplace item in Azure Stack.
services: azure-stack
documentationcenter: ''
author: rupisure
manager: byronr
editor: ''
ms.assetid: 60871cbb-eed2-433c-a76d-d605c7aec06c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: rupisure
ms.openlocfilehash: cf55ddab05fefa5b7a1b96ef2f02bcb0f83894c2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552557"
---
# <a name="the-azure-stack-marketplace"></a><span data-ttu-id="5e573-103">The Azure Stack Marketplace</span><span class="sxs-lookup"><span data-stu-id="5e573-103">The Azure Stack Marketplace</span></span>
<span data-ttu-id="5e573-104">The Marketplace is a collection of items customized for Azure Stack, like services, applications, and resources.</span><span class="sxs-lookup"><span data-stu-id="5e573-104">The Marketplace is a collection of items customized for Azure Stack, like services, applications, and resources.</span></span> <span data-ttu-id="5e573-105">It's the place where tenants come to create new resources and deploy new applications.</span><span class="sxs-lookup"><span data-stu-id="5e573-105">It's the place where tenants come to create new resources and deploy new applications.</span></span> <span data-ttu-id="5e573-106">Service administrators can add custom items to the Marketplace and tenants will see them right away.</span><span class="sxs-lookup"><span data-stu-id="5e573-106">Service administrators can add custom items to the Marketplace and tenants will see them right away.</span></span>

<span data-ttu-id="5e573-107">To open the Marketplace, click **New**.</span><span class="sxs-lookup"><span data-stu-id="5e573-107">To open the Marketplace, click **New**.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-publish-custom-marketplace-item/image1.png)

<span data-ttu-id="5e573-108">The Marketplace is updated every five minutes.</span><span class="sxs-lookup"><span data-stu-id="5e573-108">The Marketplace is updated every five minutes.</span></span>

## <a name="marketplace-items"></a><span data-ttu-id="5e573-109">Marketplace items</span><span class="sxs-lookup"><span data-stu-id="5e573-109">Marketplace items</span></span>
<span data-ttu-id="5e573-110">Every Marketplace item has:</span><span class="sxs-lookup"><span data-stu-id="5e573-110">Every Marketplace item has:</span></span>

* <span data-ttu-id="5e573-111">An Azure Resource Manager template for resource provisioning</span><span class="sxs-lookup"><span data-stu-id="5e573-111">An Azure Resource Manager template for resource provisioning</span></span>
* <span data-ttu-id="5e573-112">Metadata, like strings, icons, and other marketing collateral</span><span class="sxs-lookup"><span data-stu-id="5e573-112">Metadata, like strings, icons, and other marketing collateral</span></span>
* <span data-ttu-id="5e573-113">Formatting information to display the item in the portal</span><span class="sxs-lookup"><span data-stu-id="5e573-113">Formatting information to display the item in the portal</span></span>

<span data-ttu-id="5e573-114">Every item published to the Marketplace uses a format called the Azure Gallery Package (azpkg).</span><span class="sxs-lookup"><span data-stu-id="5e573-114">Every item published to the Marketplace uses a format called the Azure Gallery Package (azpkg).</span></span> <span data-ttu-id="5e573-115">Deployment or runtime resources (like code, zip files with software, or virtual machine images) should be added to Azure Stack separately, not as part of the Marketplace Item.</span><span class="sxs-lookup"><span data-stu-id="5e573-115">Deployment or runtime resources (like code, zip files with software, or virtual machine images) should be added to Azure Stack separately, not as part of the Marketplace Item.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5e573-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="5e573-116">Next steps</span></span>
[<span data-ttu-id="5e573-117">Create and publish a marketplace item</span><span class="sxs-lookup"><span data-stu-id="5e573-117">Create and publish a marketplace item</span></span>](azure-stack-create-and-publish-marketplace-item.md)


