---
title: Understand your Azure external service charges | Microsoft Docs
description: Learn about billing of external services, formerly known as Marketplace, charges in Azure.
services: ''
documentationcenter: ''
author: adpick
manager: ruchic
editor: ''
tags: billing
ms.assetid: 5e0e2a3c-d111-4054-8508-0c111c1b749b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: adpick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 651eaa1ba84dabf2389d8b43767910380a8f52c4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563563"
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a><span data-ttu-id="d6e4b-103">Understand your Azure billing for external service charges</span><span class="sxs-lookup"><span data-stu-id="d6e4b-103">Understand your Azure billing for external service charges</span></span>
<span data-ttu-id="d6e4b-104">External services used to be called Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-104">External services used to be called Azure Marketplace.</span></span> <span data-ttu-id="d6e4b-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span></span> <span data-ttu-id="d6e4b-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span></span>

<span data-ttu-id="d6e4b-107">When you provision a new external service or resource, a warning is shown:</span><span class="sxs-lookup"><span data-stu-id="d6e4b-107">When you provision a new external service or resource, a warning is shown:</span></span>

![Marketplace purchase warning](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> <span data-ttu-id="d6e4b-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span></span>
> 
> 

## <a name="how-external-services-are-billed"></a><span data-ttu-id="d6e4b-110">How external services are billed</span><span class="sxs-lookup"><span data-stu-id="d6e4b-110">How external services are billed</span></span>
- <span data-ttu-id="d6e4b-111">External services are billed separately.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-111">External services are billed separately.</span></span> <span data-ttu-id="d6e4b-112">They are treated as individual orders within your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-112">They are treated as individual orders within your Azure subscription.</span></span> <span data-ttu-id="d6e4b-113">The billing period for each service is set when you purchase the service.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-113">The billing period for each service is set when you purchase the service.</span></span> <span data-ttu-id="d6e4b-114">Not to be confused with the billing period of the subscription under which you purchased it.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-114">Not to be confused with the billing period of the subscription under which you purchased it.</span></span> <span data-ttu-id="d6e4b-115">You also receive separate bills and your credit card is charged separately.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-115">You also receive separate bills and your credit card is charged separately.</span></span>
- <span data-ttu-id="d6e4b-116">Each external service has a different billing model.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-116">Each external service has a different billing model.</span></span> <span data-ttu-id="d6e4b-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span></span> <span data-ttu-id="d6e4b-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span></span>
- <span data-ttu-id="d6e4b-119">You can't use monthly free credits for external services.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-119">You can't use monthly free credits for external services.</span></span> <span data-ttu-id="d6e4b-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied to external service bills.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied to external service bills.</span></span> <span data-ttu-id="d6e4b-121">Use a credit card to purchase external services.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-121">Use a credit card to purchase external services.</span></span>


## <a name="view-external-service-spending-and-history-in-the-azure-portal"></a><span data-ttu-id="d6e4b-122">View external service spending and history in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d6e4b-122">View external service spending and history in the Azure portal</span></span>
<span data-ttu-id="d6e4b-123">You can view a list of the external services that are on each subscription within the [Azure portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="d6e4b-123">You can view a list of the external services that are on each subscription within the [Azure portal](https://portal.azure.com/):</span></span> 

1. <span data-ttu-id="d6e4b-124">Sign in to the [Azure portal](https://portal.azure.com/) as the account administrator.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-124">Sign in to the [Azure portal](https://portal.azure.com/) as the account administrator.</span></span>
2. <span data-ttu-id="d6e4b-125">In the Hub menu, select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-125">In the Hub menu, select **Subscriptions**.</span></span>
   
    ![Select Subscriptions in the Hub menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. <span data-ttu-id="d6e4b-127">In the **Subscriptions** blade, select the subscription that you want to view, and then select **External services**.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-127">In the **Subscriptions** blade, select the subscription that you want to view, and then select **External services**.</span></span>
   
    ![Select a subscription in the billing blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. <span data-ttu-id="d6e4b-129">You should see each of your external service orders, the publisher name, service tier you bought, name you gave the resource, and the current order status.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-129">You should see each of your external service orders, the publisher name, service tier you bought, name you gave the resource, and the current order status.</span></span> <span data-ttu-id="d6e4b-130">To see past bills, select an external service.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-130">To see past bills, select an external service.</span></span>
   
    ![Select an external service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. <span data-ttu-id="d6e4b-132">From here, you can view past bill amounts including the tax breakdown.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-132">From here, you can view past bill amounts including the tax breakdown.</span></span>
   
    ![View external services billing history](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="d6e4b-134">View external service spending for Enterprise Agreement (EA) customers</span><span class="sxs-lookup"><span data-stu-id="d6e4b-134">View external service spending for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="d6e4b-135">EA customers can see external service spending and download reports in the EA portal.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-135">EA customers can see external service spending and download reports in the EA portal.</span></span> <span data-ttu-id="d6e4b-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) to get started.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) to get started.</span></span>

## <a name="manage-payment-methods-for-external-service-orders"></a><span data-ttu-id="d6e4b-137">Manage payment methods for external service orders</span><span class="sxs-lookup"><span data-stu-id="d6e4b-137">Manage payment methods for external service orders</span></span>
<span data-ttu-id="d6e4b-138">Update your payment methods for external service orders from the [Account Center](https://account.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="d6e4b-138">Update your payment methods for external service orders from the [Account Center](https://account.windowsazure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="d6e4b-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to make changes to your payment method.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to make changes to your payment method.</span></span>
> 
> 

1. <span data-ttu-id="d6e4b-140">Sign in to the [Account Center](https://account.windowsazure.com/) and [navigate to the **marketplace** tab](https://account.windowsazure.com/Store)</span><span class="sxs-lookup"><span data-stu-id="d6e4b-140">Sign in to the [Account Center](https://account.windowsazure.com/) and [navigate to the **marketplace** tab](https://account.windowsazure.com/Store)</span></span>
   
    ![Select marketplace in the account center](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. <span data-ttu-id="d6e4b-142">Select the external service you want to manage</span><span class="sxs-lookup"><span data-stu-id="d6e4b-142">Select the external service you want to manage</span></span>
   
    ![Select the external service you want to manage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. <span data-ttu-id="d6e4b-144">Click **Change payment method** on the right side of the page.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-144">Click **Change payment method** on the right side of the page.</span></span> <span data-ttu-id="d6e4b-145">This link brings you to a different portal to manage your payment method.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-145">This link brings you to a different portal to manage your payment method.</span></span>
   
    ![Order summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. <span data-ttu-id="d6e4b-147">Click **Edit info** and follow instructions to update your payment information.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-147">Click **Edit info** and follow instructions to update your payment information.</span></span>
   
    ![Select edit info](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a><span data-ttu-id="d6e4b-149">Cancel an external service order</span><span class="sxs-lookup"><span data-stu-id="d6e4b-149">Cancel an external service order</span></span>
<span data-ttu-id="d6e4b-150">If you want to cancel your external service order, delete the resource in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6e4b-150">If you want to cancel your external service order, delete the resource in the [Azure portal](https://portal.azure.com).</span></span>

![Delete Resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a><span data-ttu-id="d6e4b-152">Need help?</span><span class="sxs-lookup"><span data-stu-id="d6e4b-152">Need help?</span></span> <span data-ttu-id="d6e4b-153">Contact support.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-153">Contact support.</span></span>
<span data-ttu-id="d6e4b-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span><span class="sxs-lookup"><span data-stu-id="d6e4b-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>











