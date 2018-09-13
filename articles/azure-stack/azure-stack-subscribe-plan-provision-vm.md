---
title: Subscribe to an offer and then provision a VM in Azure Stack (tenant) | Microsoft Docs
description: As a tenant, learn how to subscribe to an offer and then provision a VM in Azure Stack.
services: azure-stack
documentationcenter: ''
author: ErikjeMS
manager: byronr
editor: ''
ms.assetid: 7f3f8683-ef09-4838-92ed-41f2fddbbbed
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 3/1/2017
ms.author: erikje
ms.openlocfilehash: 1e445178ce3b14b9183bff475b75cdbb8d1148b4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552839"
---
# <a name="subscribe-to-an-offer"></a><span data-ttu-id="aa412-103">Subscribe to an offer</span><span class="sxs-lookup"><span data-stu-id="aa412-103">Subscribe to an offer</span></span>
<span data-ttu-id="aa412-104">Now that you've [created an offer](azure-stack-create-offer.md), test that your tenants can create a subscription.</span><span class="sxs-lookup"><span data-stu-id="aa412-104">Now that you've [created an offer](azure-stack-create-offer.md), test that your tenants can create a subscription.</span></span>

1. <span data-ttu-id="aa412-105">On the Azure Stack POC computer, log in to `https://portal.local.azurestack.external` as [a tenant](azure-stack-connect-azure-stack.md) and click **Get a Subscription**.</span><span class="sxs-lookup"><span data-stu-id="aa412-105">On the Azure Stack POC computer, log in to `https://portal.local.azurestack.external` as [a tenant](azure-stack-connect-azure-stack.md) and click **Get a Subscription**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-subscribe-plan-provision-vm/image01.png)
2. <span data-ttu-id="aa412-106">In the **Display Name** field, type a name for your subscription, click **Offer**, click one of the offers in the **Choose an offer** blade, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="aa412-106">In the **Display Name** field, type a name for your subscription, click **Offer**, click one of the offers in the **Choose an offer** blade, and then click **Create**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-subscribe-plan-provision-vm/image02.png)
3. <span data-ttu-id="aa412-107">To view the subscription you created, click **More services**, click **Subscriptions**, then click your new subscription.</span><span class="sxs-lookup"><span data-stu-id="aa412-107">To view the subscription you created, click **More services**, click **Subscriptions**, then click your new subscription.</span></span>  

<span data-ttu-id="aa412-108">After you subscribe to an offer, refresh the portal to see which services are part of the new subscription.</span><span class="sxs-lookup"><span data-stu-id="aa412-108">After you subscribe to an offer, refresh the portal to see which services are part of the new subscription.</span></span>

# <a name="subscribe-to-an-add-on-plan"></a><span data-ttu-id="aa412-109">Subscribe to an add-on plan</span><span class="sxs-lookup"><span data-stu-id="aa412-109">Subscribe to an add-on plan</span></span>
<span data-ttu-id="aa412-110">If the offer has an add-on plan, tenants can add them to their subscription at any time.</span><span class="sxs-lookup"><span data-stu-id="aa412-110">If the offer has an add-on plan, tenants can add them to their subscription at any time.</span></span>  

1. <span data-ttu-id="aa412-111">In the tenant portal, select More services > Subscriptions .</span><span class="sxs-lookup"><span data-stu-id="aa412-111">In the tenant portal, select More services > Subscriptions .</span></span>

2. <span data-ttu-id="aa412-112">Click on the subscription > Add Plan button, and select the add-on plan.</span><span class="sxs-lookup"><span data-stu-id="aa412-112">Click on the subscription > Add Plan button, and select the add-on plan.</span></span>



## <a name="next-steps"></a><span data-ttu-id="aa412-113">Next steps</span><span class="sxs-lookup"><span data-stu-id="aa412-113">Next steps</span></span>
[<span data-ttu-id="aa412-114">Provision a virtual machine</span><span class="sxs-lookup"><span data-stu-id="aa412-114">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)


