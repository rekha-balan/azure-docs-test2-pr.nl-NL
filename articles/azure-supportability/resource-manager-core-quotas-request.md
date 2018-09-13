---
title: Azure Resource Manager vCPU quota increase requests | Microsoft Docs
description: Azure Resource Manager vCPU quota increase requests
author: ganganarayanan
ms.author: gangan
ms.date: 6/13/2018
ms.topic: article
ms.service: microsoft-docs
ms.assetid: ce37c848-ddd9-46ab-978e-6a1445728a3b
ms.openlocfilehash: 7456785815dbefb2436713814965d90ba0e789ee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44805342"
---
# <a name="resource-manager-vcpu-quota-increase-requests"></a><span data-ttu-id="e2827-103">Resource Manager vCPU quota increase requests</span><span class="sxs-lookup"><span data-stu-id="e2827-103">Resource Manager vCPU quota increase requests</span></span>

<span data-ttu-id="e2827-104">Resource Manager vCPU quotas are enforced at the region level and SKU family level.</span><span class="sxs-lookup"><span data-stu-id="e2827-104">Resource Manager vCPU quotas are enforced at the region level and SKU family level.</span></span>
<span data-ttu-id="e2827-105">Learn more about how quotas are enforced on the [Azure subscription and service limits](http://aka.ms/quotalimits) page.</span><span class="sxs-lookup"><span data-stu-id="e2827-105">Learn more about how quotas are enforced on the [Azure subscription and service limits](http://aka.ms/quotalimits) page.</span></span>
<span data-ttu-id="e2827-106">To learn more about SKU Families, you may compare cost and performance on the [Virtual Machines Pricing](http://aka.ms/pricingcompute) page.</span><span class="sxs-lookup"><span data-stu-id="e2827-106">To learn more about SKU Families, you may compare cost and performance on the [Virtual Machines Pricing](http://aka.ms/pricingcompute) page.</span></span>

<span data-ttu-id="e2827-107">To request an increase, follow the instructions below using to create a support request via Azure's 'Usage + quota' blade available in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e2827-107">To request an increase, follow the instructions below using to create a support request via Azure's 'Usage + quota' blade available in the Azure Portal.</span></span> 

## <a name="request-quota-increase-at-subscription-level"></a><span data-ttu-id="e2827-108">Request quota increase at subscription level</span><span class="sxs-lookup"><span data-stu-id="e2827-108">Request quota increase at subscription level</span></span>

1. <span data-ttu-id="e2827-109">From https://portal.azure.com, select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="e2827-109">From https://portal.azure.com, select **Subscriptions**.</span></span>

   ![Subscriptions](./media/resource-manager-core-quotas-request/subscriptions.png)

2. <span data-ttu-id="e2827-111">Select the subscription that needs an increased quota.</span><span class="sxs-lookup"><span data-stu-id="e2827-111">Select the subscription that needs an increased quota.</span></span>

   ![Select subscription](./media/resource-manager-core-quotas-request/select-subscription.png)

3. <span data-ttu-id="e2827-113">Select **Usage + quotas**</span><span class="sxs-lookup"><span data-stu-id="e2827-113">Select **Usage + quotas**</span></span>

   ![Select usage and quotas](./media/resource-manager-core-quotas-request/select-usage-quotas.png)

4. <span data-ttu-id="e2827-115">In the upper right corner, select **Request increase**.</span><span class="sxs-lookup"><span data-stu-id="e2827-115">In the upper right corner, select **Request increase**.</span></span>

   ![Request increase](./media/resource-manager-core-quotas-request/request-increase.png)

5. <span data-ttu-id="e2827-117">Step:1 - Select **Cores** as the quote type.</span><span class="sxs-lookup"><span data-stu-id="e2827-117">Step:1 - Select **Cores** as the quote type.</span></span> 

   ![Fill in form](./media/resource-manager-core-quotas-request/forms.png)
   
6. <span data-ttu-id="e2827-119">Step:2 - Select Deployment model as "Resource Manager" and select a location.</span><span class="sxs-lookup"><span data-stu-id="e2827-119">Step:2 - Select Deployment model as "Resource Manager" and select a location.</span></span>

    ![Quota Problem blade](./media/resource-manager-core-quotas-request/Problem-step.png)

3. <span data-ttu-id="e2827-121">Select the SKU Families that require an increase.</span><span class="sxs-lookup"><span data-stu-id="e2827-121">Select the SKU Families that require an increase.</span></span>

    ![SKU series selected](./media/resource-manager-core-quotas-request/SKU-selected.png)

4. <span data-ttu-id="e2827-123">Enter the new limits you would like on the subscription.</span><span class="sxs-lookup"><span data-stu-id="e2827-123">Enter the new limits you would like on the subscription.</span></span>

    ![SKU new quota request](./media/resource-manager-core-quotas-request/SKU-new-quota.png)

- <span data-ttu-id="e2827-125">To remove a line, uncheck the SKU from the SKU family dropdown or click the discard "x" icon.</span><span class="sxs-lookup"><span data-stu-id="e2827-125">To remove a line, uncheck the SKU from the SKU family dropdown or click the discard "x" icon.</span></span>
<span data-ttu-id="e2827-126">After entering the desired quota for each SKU family, click "Next" on the Problem step page to continue with the support request creation.</span><span class="sxs-lookup"><span data-stu-id="e2827-126">After entering the desired quota for each SKU family, click "Next" on the Problem step page to continue with the support request creation.</span></span>

