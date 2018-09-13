---
title: Create an offer in Azure Stack | Microsoft Docs
description: As a service administrator, learn how to create an offer for your tenants in Azure Stack.
services: azure-stack
documentationcenter: ''
author: ErikjeMS
manager: byronr
editor: ''
ms.assetid: 96b080a4-a9a5-407c-ba54-111de2413d59
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/26/2016
ms.author: erikje
ms.openlocfilehash: 0826c66d29be42b039fd21b431e2d33917acf0e1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660941"
---
# <a name="create-an-offer-in-azure-stack"></a><span data-ttu-id="fd576-103">Create an offer in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="fd576-103">Create an offer in Azure Stack</span></span>
<span data-ttu-id="fd576-104">[Offers](azure-stack-key-features.md) are groups of one or more plans that providers present to tenants to purchase or subscribe to.</span><span class="sxs-lookup"><span data-stu-id="fd576-104">[Offers](azure-stack-key-features.md) are groups of one or more plans that providers present to tenants to purchase or subscribe to.</span></span> <span data-ttu-id="fd576-105">This document shows you how to create an offer that includes the [plan that you created](azure-stack-create-plan.md) in the last step.</span><span class="sxs-lookup"><span data-stu-id="fd576-105">This document shows you how to create an offer that includes the [plan that you created](azure-stack-create-plan.md) in the last step.</span></span> <span data-ttu-id="fd576-106">This offer gives subscribers the ability to provision virtual machines.</span><span class="sxs-lookup"><span data-stu-id="fd576-106">This offer gives subscribers the ability to provision virtual machines.</span></span>

1. <span data-ttu-id="fd576-107">[Sign in](azure-stack-connect-azure-stack.md) to the portal as a service administrator and then click **New** > **Tenant Offers + Plans** > **Offer**.</span><span class="sxs-lookup"><span data-stu-id="fd576-107">[Sign in](azure-stack-connect-azure-stack.md) to the portal as a service administrator and then click **New** > **Tenant Offers + Plans** > **Offer**.</span></span>
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-offer/image01.png)
2. <span data-ttu-id="fd576-108">In the **New Offer** blade, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span><span class="sxs-lookup"><span data-stu-id="fd576-108">In the **New Offer** blade, fill in **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="fd576-109">The Display Name is the offer's friendly name.</span><span class="sxs-lookup"><span data-stu-id="fd576-109">The Display Name is the offer's friendly name.</span></span> <span data-ttu-id="fd576-110">Only the admin can see the Resource Name.</span><span class="sxs-lookup"><span data-stu-id="fd576-110">Only the admin can see the Resource Name.</span></span> <span data-ttu-id="fd576-111">It's the name that admins use to work with the offer as an Azure Resource Manager resource.</span><span class="sxs-lookup"><span data-stu-id="fd576-111">It's the name that admins use to work with the offer as an Azure Resource Manager resource.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-offer/image01a.png)
3. <span data-ttu-id="fd576-112">Click **Base plans** and, in the **Plan** blade, select the plans you want to include in the offer, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="fd576-112">Click **Base plans** and, in the **Plan** blade, select the plans you want to include in the offer, and then click **Select**.</span></span> <span data-ttu-id="fd576-113">Click **Create** to create the offer.</span><span class="sxs-lookup"><span data-stu-id="fd576-113">Click **Create** to create the offer.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-offer/image02.png)
4. <span data-ttu-id="fd576-114">Click **Offers** and then click the offer you just created.</span><span class="sxs-lookup"><span data-stu-id="fd576-114">Click **Offers** and then click the offer you just created.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-offer/image03.png)
5. <span data-ttu-id="fd576-115">Click **Change State**, and then click **Public**.</span><span class="sxs-lookup"><span data-stu-id="fd576-115">Click **Change State**, and then click **Public**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-offer/image04.png)

<span data-ttu-id="fd576-116">Offers must be made public for tenants to get the full view when subscribing.</span><span class="sxs-lookup"><span data-stu-id="fd576-116">Offers must be made public for tenants to get the full view when subscribing.</span></span> <span data-ttu-id="fd576-117">Offers can be:</span><span class="sxs-lookup"><span data-stu-id="fd576-117">Offers can be:</span></span>

* <span data-ttu-id="fd576-118">**Public**: Visible to tenants.</span><span class="sxs-lookup"><span data-stu-id="fd576-118">**Public**: Visible to tenants.</span></span>
* <span data-ttu-id="fd576-119">**Private**: Only visible to the service administrators.</span><span class="sxs-lookup"><span data-stu-id="fd576-119">**Private**: Only visible to the service administrators.</span></span> <span data-ttu-id="fd576-120">Useful while drafting the plan or offer, or if the service administrator wants to approve every subscription.</span><span class="sxs-lookup"><span data-stu-id="fd576-120">Useful while drafting the plan or offer, or if the service administrator wants to approve every subscription.</span></span>
* <span data-ttu-id="fd576-121">**Decommissioned**: Closed to new subscribers.</span><span class="sxs-lookup"><span data-stu-id="fd576-121">**Decommissioned**: Closed to new subscribers.</span></span> <span data-ttu-id="fd576-122">The service administrator can use decommissioned to prevent future subscriptions, but leave current subscribers untouched.</span><span class="sxs-lookup"><span data-stu-id="fd576-122">The service administrator can use decommissioned to prevent future subscriptions, but leave current subscribers untouched.</span></span>

<span data-ttu-id="fd576-123">Changes to the offer are not immediately visible to the tenant.</span><span class="sxs-lookup"><span data-stu-id="fd576-123">Changes to the offer are not immediately visible to the tenant.</span></span> <span data-ttu-id="fd576-124">To see the changes, you might have to logout/login to see the new subscription in the “Subscription picker” when creating resources/resource groups.</span><span class="sxs-lookup"><span data-stu-id="fd576-124">To see the changes, you might have to logout/login to see the new subscription in the “Subscription picker” when creating resources/resource groups.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd576-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="fd576-125">Next steps</span></span>
[<span data-ttu-id="fd576-126">Subscribe to an offer and then provision a VM</span><span class="sxs-lookup"><span data-stu-id="fd576-126">Subscribe to an offer and then provision a VM</span></span>](azure-stack-subscribe-plan-provision-vm.md)





