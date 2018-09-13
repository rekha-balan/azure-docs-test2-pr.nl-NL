---
title: Subscribe to an offer in Azure Stack | Microsoft Docs
description: Create subscriptions for offers in Azure Stack
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: 7f3f8683-ef09-4838-92ed-41f2fddbbbed
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/05/2018
ms.author: brenduns
ms.openlocfilehash: b35e75d7cfcaa46da46d2edcb80fe37c112a66a3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783866"
---
# <a name="create-subscriptions-to-offers-in-azure-stack"></a><span data-ttu-id="fd57f-103">Create subscriptions to offers in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="fd57f-103">Create subscriptions to offers in Azure Stack</span></span>

<span data-ttu-id="fd57f-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="fd57f-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="fd57f-105">After you [create an offer](azure-stack-create-offer.md), users need a subscription to that offer before they can use it.</span><span class="sxs-lookup"><span data-stu-id="fd57f-105">After you [create an offer](azure-stack-create-offer.md), users need a subscription to that offer before they can use it.</span></span> <span data-ttu-id="fd57f-106">There are two ways that users can get subscribed to an offer:</span><span class="sxs-lookup"><span data-stu-id="fd57f-106">There are two ways that users can get subscribed to an offer:</span></span>

- <span data-ttu-id="fd57f-107">As a cloud operator, you can create a subscription for a user from within the administrator portal.</span><span class="sxs-lookup"><span data-stu-id="fd57f-107">As a cloud operator, you can create a subscription for a user from within the administrator portal.</span></span> <span data-ttu-id="fd57f-108">Subscriptions you create can be for both public and private offers.</span><span class="sxs-lookup"><span data-stu-id="fd57f-108">Subscriptions you create can be for both public and private offers.</span></span>
- <span data-ttu-id="fd57f-109">As a tenant user, you can subscribe to a public offer when you use the user portal.</span><span class="sxs-lookup"><span data-stu-id="fd57f-109">As a tenant user, you can subscribe to a public offer when you use the user portal.</span></span>  

## <a name="create-a-subscription-as-a-cloud-operator"></a><span data-ttu-id="fd57f-110">Create a subscription as a cloud operator</span><span class="sxs-lookup"><span data-stu-id="fd57f-110">Create a subscription as a cloud operator</span></span>

<span data-ttu-id="fd57f-111">Cloud operators can use the admin portal to create a subscription to an offer for a user.</span><span class="sxs-lookup"><span data-stu-id="fd57f-111">Cloud operators can use the admin portal to create a subscription to an offer for a user.</span></span>  <span data-ttu-id="fd57f-112">You can create subscriptions for members of your own directory tenant.</span><span class="sxs-lookup"><span data-stu-id="fd57f-112">You can create subscriptions for members of your own directory tenant.</span></span>  <span data-ttu-id="fd57f-113">When [multi-tenancy](azure-stack-enable-multitenancy.md) is enabled, you can also create subscriptions for users in additional directory tenants.</span><span class="sxs-lookup"><span data-stu-id="fd57f-113">When [multi-tenancy](azure-stack-enable-multitenancy.md) is enabled, you can also create subscriptions for users in additional directory tenants.</span></span>

<span data-ttu-id="fd57f-114">If don't want your tenants to create their own subscriptions, make your offers private, and then create subscriptions for your tenants.</span><span class="sxs-lookup"><span data-stu-id="fd57f-114">If don't want your tenants to create their own subscriptions, make your offers private, and then create subscriptions for your tenants.</span></span> <span data-ttu-id="fd57f-115">This approach is common when integrating Azure Stack with external billing or service catalog systems.</span><span class="sxs-lookup"><span data-stu-id="fd57f-115">This approach is common when integrating Azure Stack with external billing or service catalog systems.</span></span>

<span data-ttu-id="fd57f-116">After you create a subscription for a user, they can sign in to the user portal and see that they're subscribed to the offer.</span><span class="sxs-lookup"><span data-stu-id="fd57f-116">After you create a subscription for a user, they can sign in to the user portal and see that they're subscribed to the offer.</span></span>  

### <a name="to-create-a-subscription-for-a-user"></a><span data-ttu-id="fd57f-117">To create a subscription for a user</span><span class="sxs-lookup"><span data-stu-id="fd57f-117">To create a subscription for a user</span></span>

1. <span data-ttu-id="fd57f-118">In the Admin portal, go to **User subscriptions.**</span><span class="sxs-lookup"><span data-stu-id="fd57f-118">In the Admin portal, go to **User subscriptions.**</span></span>
2. <span data-ttu-id="fd57f-119">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="fd57f-119">Select **Add**.</span></span> <span data-ttu-id="fd57f-120">Under **New user subscription**, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="fd57f-120">Under **New user subscription**, enter the following information:</span></span>  

   - <span data-ttu-id="fd57f-121">**Display name** – A friendly name for identifying the subscription that appears as the *User subscription name*.</span><span class="sxs-lookup"><span data-stu-id="fd57f-121">**Display name** – A friendly name for identifying the subscription that appears as the *User subscription name*.</span></span>
   - <span data-ttu-id="fd57f-122">**User** – Specify a user from an available directory tenant for this subscription.</span><span class="sxs-lookup"><span data-stu-id="fd57f-122">**User** – Specify a user from an available directory tenant for this subscription.</span></span> <span data-ttu-id="fd57f-123">The user name appears as *Owner*.</span><span class="sxs-lookup"><span data-stu-id="fd57f-123">The user name appears as *Owner*.</span></span>  <span data-ttu-id="fd57f-124">The format of the user name depends on your identity solution.</span><span class="sxs-lookup"><span data-stu-id="fd57f-124">The format of the user name depends on your identity solution.</span></span> <span data-ttu-id="fd57f-125">For example:</span><span class="sxs-lookup"><span data-stu-id="fd57f-125">For example:</span></span>

     - <span data-ttu-id="fd57f-126">**Azure AD:** `<user1>@<contoso.onmicrosoft.com>`</span><span class="sxs-lookup"><span data-stu-id="fd57f-126">**Azure AD:** `<user1>@<contoso.onmicrosoft.com>`</span></span>

     - <span data-ttu-id="fd57f-127">**AD FS:** `<user1>@<azurestack.local>`</span><span class="sxs-lookup"><span data-stu-id="fd57f-127">**AD FS:** `<user1>@<azurestack.local>`</span></span> 

   - <span data-ttu-id="fd57f-128">**Directory tenant** –  Select the directory tenant where the user account belongs.</span><span class="sxs-lookup"><span data-stu-id="fd57f-128">**Directory tenant** –  Select the directory tenant where the user account belongs.</span></span> <span data-ttu-id="fd57f-129">If you haven't enabled multi-tenancy, only your local directory tenant is available.</span><span class="sxs-lookup"><span data-stu-id="fd57f-129">If you haven't enabled multi-tenancy, only your local directory tenant is available.</span></span>

3. <span data-ttu-id="fd57f-130">Select **Offer**.</span><span class="sxs-lookup"><span data-stu-id="fd57f-130">Select **Offer**.</span></span> <span data-ttu-id="fd57f-131">Under **Offers**, choose an **Offer** for this subscription.</span><span class="sxs-lookup"><span data-stu-id="fd57f-131">Under **Offers**, choose an **Offer** for this subscription.</span></span> <span data-ttu-id="fd57f-132">Because you're creating the subscription for a user, select **Private** as the Accessibility state.</span><span class="sxs-lookup"><span data-stu-id="fd57f-132">Because you're creating the subscription for a user, select **Private** as the Accessibility state.</span></span>

4. <span data-ttu-id="fd57f-133">Select **Create** to create the subscription.</span><span class="sxs-lookup"><span data-stu-id="fd57f-133">Select **Create** to create the subscription.</span></span> <span data-ttu-id="fd57f-134">You'll see the new subscription under **User subscription**.</span><span class="sxs-lookup"><span data-stu-id="fd57f-134">You'll see the new subscription under **User subscription**.</span></span> <span data-ttu-id="fd57f-135">When the user  signs in to the user portal they can see the subscription details.</span><span class="sxs-lookup"><span data-stu-id="fd57f-135">When the user  signs in to the user portal they can see the subscription details.</span></span>

### <a name="to-make-an-add-on-plan-available"></a><span data-ttu-id="fd57f-136">To make an add-on plan available</span><span class="sxs-lookup"><span data-stu-id="fd57f-136">To make an add-on plan available</span></span>

<span data-ttu-id="fd57f-137">A cloud operator can add an add-on plan to a previously created subscription at any time:</span><span class="sxs-lookup"><span data-stu-id="fd57f-137">A cloud operator can add an add-on plan to a previously created subscription at any time:</span></span>

1. <span data-ttu-id="fd57f-138">In the admin portal, select **All Services** and then under the **ADMINISTRATIVE RESOURCES** category, select **User subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="fd57f-138">In the admin portal, select **All Services** and then under the **ADMINISTRATIVE RESOURCES** category, select **User subscriptions**.</span></span> <span data-ttu-id="fd57f-139">Select the subscription you want to change.</span><span class="sxs-lookup"><span data-stu-id="fd57f-139">Select the subscription you want to change.</span></span>

2. <span data-ttu-id="fd57f-140">Select **Add-ons**  and then select **+Add**.</span><span class="sxs-lookup"><span data-stu-id="fd57f-140">Select **Add-ons**  and then select **+Add**.</span></span>  

3. <span data-ttu-id="fd57f-141">Under **Add plan**, select the plan you want as an add-on.</span><span class="sxs-lookup"><span data-stu-id="fd57f-141">Under **Add plan**, select the plan you want as an add-on.</span></span>

## <a name="create-a-subscription-as-a-user"></a><span data-ttu-id="fd57f-142">Create a subscription as a user</span><span class="sxs-lookup"><span data-stu-id="fd57f-142">Create a subscription as a user</span></span>

<span data-ttu-id="fd57f-143">As a user, you can sign in to the user portal to locate and subscribe to public offers and add-on plans for your directory tenant (organization).</span><span class="sxs-lookup"><span data-stu-id="fd57f-143">As a user, you can sign in to the user portal to locate and subscribe to public offers and add-on plans for your directory tenant (organization).</span></span>

>[!NOTE]
><span data-ttu-id="fd57f-144">If your Azure Stack environment supports [multi-tenancy](azure-stack-enable-multitenancy.md) you can also subscribe to offers from a remote directory tenant.</span><span class="sxs-lookup"><span data-stu-id="fd57f-144">If your Azure Stack environment supports [multi-tenancy](azure-stack-enable-multitenancy.md) you can also subscribe to offers from a remote directory tenant.</span></span>

### <a name="to-subscribe-to-an-offer"></a><span data-ttu-id="fd57f-145">To subscribe to an offer</span><span class="sxs-lookup"><span data-stu-id="fd57f-145">To subscribe to an offer</span></span>

1. <span data-ttu-id="fd57f-146">[Sign in](azure-stack-connect-azure-stack.md) to the Azure Stack user portal (https://portal.local.azurestack.external) and select **Get a Subscription**.</span><span class="sxs-lookup"><span data-stu-id="fd57f-146">[Sign in](azure-stack-connect-azure-stack.md) to the Azure Stack user portal (https://portal.local.azurestack.external) and select **Get a Subscription**.</span></span>

   ![Get a subscription](media/azure-stack-subscribe-plan-provision-vm/image01.png)
  
2. <span data-ttu-id="fd57f-148">Under **Get a subscription**, enter the friendly name of the subscription in **Display Name**.</span><span class="sxs-lookup"><span data-stu-id="fd57f-148">Under **Get a subscription**, enter the friendly name of the subscription in **Display Name**.</span></span> <span data-ttu-id="fd57f-149">Select **Offer** and under **Choose an offer**, pick an offer.</span><span class="sxs-lookup"><span data-stu-id="fd57f-149">Select **Offer** and under **Choose an offer**, pick an offer.</span></span> <span data-ttu-id="fd57f-150">Select **Create** to create the subscription.</span><span class="sxs-lookup"><span data-stu-id="fd57f-150">Select **Create** to create the subscription.</span></span>

   ![Create an offer](media/azure-stack-subscribe-plan-provision-vm/image02.png)
  
3. <span data-ttu-id="fd57f-152">After you subscribe to an offer, refresh the portal to see which services are part of the new subscription.</span><span class="sxs-lookup"><span data-stu-id="fd57f-152">After you subscribe to an offer, refresh the portal to see which services are part of the new subscription.</span></span>
4. <span data-ttu-id="fd57f-153">To see the subscription you created, select **All services** and then under the **GENERAL** category select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="fd57f-153">To see the subscription you created, select **All services** and then under the **GENERAL** category select **Subscriptions**.</span></span> <span data-ttu-id="fd57f-154">Select the subscription to see the subscription details.</span><span class="sxs-lookup"><span data-stu-id="fd57f-154">Select the subscription to see the subscription details.</span></span>  

### <a name="to-subscribe-to-an-add-on-plan"></a><span data-ttu-id="fd57f-155">To subscribe to an add-on plan</span><span class="sxs-lookup"><span data-stu-id="fd57f-155">To subscribe to an add-on plan</span></span>

<span data-ttu-id="fd57f-156">If an offer has an add-on plan, you can add that plan to your subscription at any time.</span><span class="sxs-lookup"><span data-stu-id="fd57f-156">If an offer has an add-on plan, you can add that plan to your subscription at any time.</span></span>  

1. <span data-ttu-id="fd57f-157">In the user portal, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="fd57f-157">In the user portal, select **All services**.</span></span> <span data-ttu-id="fd57f-158">Next, under the **GENERAL** category select **Subscriptions**, and then select the subscription that you want change.</span><span class="sxs-lookup"><span data-stu-id="fd57f-158">Next, under the **GENERAL** category select **Subscriptions**, and then select the subscription that you want change.</span></span> <span data-ttu-id="fd57f-159">If there are any add-on plans available, **+Add plan** is active and there's a tile for **Add-on plans**.</span><span class="sxs-lookup"><span data-stu-id="fd57f-159">If there are any add-on plans available, **+Add plan** is active and there's a tile for **Add-on plans**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="fd57f-160">If **+Add plan** isn't active, then there aren't any add-on plans for the offer associated with that subscription.</span><span class="sxs-lookup"><span data-stu-id="fd57f-160">If **+Add plan** isn't active, then there aren't any add-on plans for the offer associated with that subscription.</span></span>

1. <span data-ttu-id="fd57f-161">Select **+Add plan** or the **Add-on plans** tile.</span><span class="sxs-lookup"><span data-stu-id="fd57f-161">Select **+Add plan** or the **Add-on plans** tile.</span></span> <span data-ttu-id="fd57f-162">Under **Add-on plans**, select the plan you want to add.</span><span class="sxs-lookup"><span data-stu-id="fd57f-162">Under **Add-on plans**, select the plan you want to add.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd57f-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="fd57f-163">Next steps</span></span>

[<span data-ttu-id="fd57f-164">Provision a virtual machine</span><span class="sxs-lookup"><span data-stu-id="fd57f-164">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
