---
title: Azure Stack plan, offer, quota, and subscription overview | Microsoft Docs
description: As a cloud operator, I want to understand Azure Stack plans, offers, quotas, and subscriptions.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: 3dc92e5c-c004-49db-9a94-783f1f798b98
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/07/2018
ms.author: brenduns
ms.reviewer: ''
ms.openlocfilehash: d8aef778807d3a8a61cf9eedaae24abce84a19ab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868681"
---
# <a name="plan-offer-quota-and-subscription-overview"></a><span data-ttu-id="0c742-103">Plan, offer, quota, and subscription overview</span><span class="sxs-lookup"><span data-stu-id="0c742-103">Plan, offer, quota, and subscription overview</span></span>

<span data-ttu-id="0c742-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="0c742-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="0c742-105">[Azure Stack](azure-stack-poc.md) lets you deliver a wide variety of services, like virtual machines, SQL Server databases, SharePoint, Exchange, and even [Azure Marketplace items](azure-stack-marketplace-azure-items.md).</span><span class="sxs-lookup"><span data-stu-id="0c742-105">[Azure Stack](azure-stack-poc.md) lets you deliver a wide variety of services, like virtual machines, SQL Server databases, SharePoint, Exchange, and even [Azure Marketplace items](azure-stack-marketplace-azure-items.md).</span></span> <span data-ttu-id="0c742-106">As an Azure Stack operator, you configure and deliver such services in Azure Stack by using plans, offers, and quotas.</span><span class="sxs-lookup"><span data-stu-id="0c742-106">As an Azure Stack operator, you configure and deliver such services in Azure Stack by using plans, offers, and quotas.</span></span>

<span data-ttu-id="0c742-107">Offers contain one or more plans, and each plan includes one or more services.</span><span class="sxs-lookup"><span data-stu-id="0c742-107">Offers contain one or more plans, and each plan includes one or more services.</span></span> <span data-ttu-id="0c742-108">By creating plans and combining them into different offers, you can manage:</span><span class="sxs-lookup"><span data-stu-id="0c742-108">By creating plans and combining them into different offers, you can manage:</span></span>

- <span data-ttu-id="0c742-109">Which services and resources your users can access.</span><span class="sxs-lookup"><span data-stu-id="0c742-109">Which services and resources your users can access.</span></span>
- <span data-ttu-id="0c742-110">The amount of resources that users can consume.</span><span class="sxs-lookup"><span data-stu-id="0c742-110">The amount of resources that users can consume.</span></span>
- <span data-ttu-id="0c742-111">Which regions have access to the resources.</span><span class="sxs-lookup"><span data-stu-id="0c742-111">Which regions have access to the resources.</span></span>

<span data-ttu-id="0c742-112">When you deliver a service, follow these high-level steps:</span><span class="sxs-lookup"><span data-stu-id="0c742-112">When you deliver a service, follow these high-level steps:</span></span>

1. <span data-ttu-id="0c742-113">Add a service that you want to deliver to your users.</span><span class="sxs-lookup"><span data-stu-id="0c742-113">Add a service that you want to deliver to your users.</span></span>
2. <span data-ttu-id="0c742-114">Create a plan that has one or more services.</span><span class="sxs-lookup"><span data-stu-id="0c742-114">Create a plan that has one or more services.</span></span> <span data-ttu-id="0c742-115">When creating a plan, select or create quotas that define the resource limits of each service in the plan.</span><span class="sxs-lookup"><span data-stu-id="0c742-115">When creating a plan, select or create quotas that define the resource limits of each service in the plan.</span></span>
3. <span data-ttu-id="0c742-116">Create an offer that contains one or more plans.</span><span class="sxs-lookup"><span data-stu-id="0c742-116">Create an offer that contains one or more plans.</span></span> <span data-ttu-id="0c742-117">The offer can include base plans and optional add-on plans.</span><span class="sxs-lookup"><span data-stu-id="0c742-117">The offer can include base plans and optional add-on plans.</span></span>

<span data-ttu-id="0c742-118">After you've created the offer, your users can subscribe to it to access the services and resources the offer provides.</span><span class="sxs-lookup"><span data-stu-id="0c742-118">After you've created the offer, your users can subscribe to it to access the services and resources the offer provides.</span></span> <span data-ttu-id="0c742-119">Users can subscribe to as many offers as they want.</span><span class="sxs-lookup"><span data-stu-id="0c742-119">Users can subscribe to as many offers as they want.</span></span> <span data-ttu-id="0c742-120">The following diagram shows a simple example of a user who has subscribed to two offers.</span><span class="sxs-lookup"><span data-stu-id="0c742-120">The following diagram shows a simple example of a user who has subscribed to two offers.</span></span> <span data-ttu-id="0c742-121">Each offer has a plan or two, and each plan gives them access to services.</span><span class="sxs-lookup"><span data-stu-id="0c742-121">Each offer has a plan or two, and each plan gives them access to services.</span></span>

![Tenant subscription with offers and plans](media/azure-stack-key-features/image4.png)

## <a name="plans"></a><span data-ttu-id="0c742-123">Plans</span><span class="sxs-lookup"><span data-stu-id="0c742-123">Plans</span></span>

<span data-ttu-id="0c742-124">Plans are groupings of one or more services.</span><span class="sxs-lookup"><span data-stu-id="0c742-124">Plans are groupings of one or more services.</span></span> <span data-ttu-id="0c742-125">As an Azure Stack operator, you [create plans](azure-stack-create-plan.md) to offer to your users.</span><span class="sxs-lookup"><span data-stu-id="0c742-125">As an Azure Stack operator, you [create plans](azure-stack-create-plan.md) to offer to your users.</span></span> <span data-ttu-id="0c742-126">In turn, your users subscribe to your offers to use the plans and services they include.</span><span class="sxs-lookup"><span data-stu-id="0c742-126">In turn, your users subscribe to your offers to use the plans and services they include.</span></span> <span data-ttu-id="0c742-127">When creating plans, make sure to set your quotas, define your base plans, and consider including optional add-on plans.</span><span class="sxs-lookup"><span data-stu-id="0c742-127">When creating plans, make sure to set your quotas, define your base plans, and consider including optional add-on plans.</span></span>

### <a name="quotas"></a><span data-ttu-id="0c742-128">Quotas</span><span class="sxs-lookup"><span data-stu-id="0c742-128">Quotas</span></span>

<span data-ttu-id="0c742-129">To help you manage your cloud capacity, you can use pre-configured quotas or create a new quota for each service in a plan.</span><span class="sxs-lookup"><span data-stu-id="0c742-129">To help you manage your cloud capacity, you can use pre-configured quotas or create a new quota for each service in a plan.</span></span> <span data-ttu-id="0c742-130">Quotas define the upper resource limits that a user subscription can provision or consume.</span><span class="sxs-lookup"><span data-stu-id="0c742-130">Quotas define the upper resource limits that a user subscription can provision or consume.</span></span> <span data-ttu-id="0c742-131">For example, a quota might allow a user to create up to five virtual machines (VMs).</span><span class="sxs-lookup"><span data-stu-id="0c742-131">For example, a quota might allow a user to create up to five virtual machines (VMs).</span></span> <span data-ttu-id="0c742-132">You set additional quotas on the virtual machines, such as RAM and CPU cores.</span><span class="sxs-lookup"><span data-stu-id="0c742-132">You set additional quotas on the virtual machines, such as RAM and CPU cores.</span></span>

<span data-ttu-id="0c742-133">You can configure quotas by region.</span><span class="sxs-lookup"><span data-stu-id="0c742-133">You can configure quotas by region.</span></span> <span data-ttu-id="0c742-134">For example, a plan that provides compute services for Region A could have a quota of two VMs with 4-GB RAM, and 8 CPU cores.</span><span class="sxs-lookup"><span data-stu-id="0c742-134">For example, a plan that provides compute services for Region A could have a quota of two VMs with 4-GB RAM, and 8 CPU cores.</span></span>

>[!NOTE]
><span data-ttu-id="0c742-135">In the Azure Stack Development Kit, only one region (named *local*) is available.</span><span class="sxs-lookup"><span data-stu-id="0c742-135">In the Azure Stack Development Kit, only one region (named *local*) is available.</span></span>

<span data-ttu-id="0c742-136">Learn more about [quota types in Azure Stack](azure-stack-quota-types.md).</span><span class="sxs-lookup"><span data-stu-id="0c742-136">Learn more about [quota types in Azure Stack](azure-stack-quota-types.md).</span></span>

### <a name="base-plan"></a><span data-ttu-id="0c742-137">Base plan</span><span class="sxs-lookup"><span data-stu-id="0c742-137">Base plan</span></span>

<span data-ttu-id="0c742-138">When creating an offer, the service administrator can include a base plan.</span><span class="sxs-lookup"><span data-stu-id="0c742-138">When creating an offer, the service administrator can include a base plan.</span></span> <span data-ttu-id="0c742-139">These base plans are included by default when a user subscribes to that offer.</span><span class="sxs-lookup"><span data-stu-id="0c742-139">These base plans are included by default when a user subscribes to that offer.</span></span> <span data-ttu-id="0c742-140">When a user subscribes, they have access to all the resource providers specified in those base plans (with the corresponding quotas.)</span><span class="sxs-lookup"><span data-stu-id="0c742-140">When a user subscribes, they have access to all the resource providers specified in those base plans (with the corresponding quotas.)</span></span>

### <a name="add-on-plans"></a><span data-ttu-id="0c742-141">Add-on plans</span><span class="sxs-lookup"><span data-stu-id="0c742-141">Add-on plans</span></span>

<span data-ttu-id="0c742-142">Add-on plans are optional plans you add to an offer.</span><span class="sxs-lookup"><span data-stu-id="0c742-142">Add-on plans are optional plans you add to an offer.</span></span> <span data-ttu-id="0c742-143">Add-on plans aren't included by default in the subscription.</span><span class="sxs-lookup"><span data-stu-id="0c742-143">Add-on plans aren't included by default in the subscription.</span></span> <span data-ttu-id="0c742-144">Add-on plans are additional plans (with quotas) available in an offer that a subscriber can add to their subscriptions.</span><span class="sxs-lookup"><span data-stu-id="0c742-144">Add-on plans are additional plans (with quotas) available in an offer that a subscriber can add to their subscriptions.</span></span> <span data-ttu-id="0c742-145">For example, you can offer a base plan with limited resources for a trial, and an add-on plan with more substantial resources to customers who decide to adopt the service.</span><span class="sxs-lookup"><span data-stu-id="0c742-145">For example, you can offer a base plan with limited resources for a trial, and an add-on plan with more substantial resources to customers who decide to adopt the service.</span></span>

## <a name="offers"></a><span data-ttu-id="0c742-146">Offers</span><span class="sxs-lookup"><span data-stu-id="0c742-146">Offers</span></span>

<span data-ttu-id="0c742-147">Offers are groups of one or more plans that you create so that users can subscribe to them.</span><span class="sxs-lookup"><span data-stu-id="0c742-147">Offers are groups of one or more plans that you create so that users can subscribe to them.</span></span> <span data-ttu-id="0c742-148">For example, Offer Alpha can contain Plan A, which provides a set of compute services and Plan B, which provides a set of storage and network services.</span><span class="sxs-lookup"><span data-stu-id="0c742-148">For example, Offer Alpha can contain Plan A, which provides a set of compute services and Plan B, which provides a set of storage and network services.</span></span>

<span data-ttu-id="0c742-149">When you [create an offer](azure-stack-create-offer.md), you must include at least one base plan, but you can also create add-on plans that users can add to their subscription.</span><span class="sxs-lookup"><span data-stu-id="0c742-149">When you [create an offer](azure-stack-create-offer.md), you must include at least one base plan, but you can also create add-on plans that users can add to their subscription.</span></span>

## <a name="subscriptions"></a><span data-ttu-id="0c742-150">Subscriptions</span><span class="sxs-lookup"><span data-stu-id="0c742-150">Subscriptions</span></span>

<span data-ttu-id="0c742-151">A subscription is how users access your offers.</span><span class="sxs-lookup"><span data-stu-id="0c742-151">A subscription is how users access your offers.</span></span> <span data-ttu-id="0c742-152">If you’re an Azure Stack operator for a service provider, your users (tenants) buy your services by subscribing to your offers.</span><span class="sxs-lookup"><span data-stu-id="0c742-152">If you’re an Azure Stack operator for a service provider, your users (tenants) buy your services by subscribing to your offers.</span></span> <span data-ttu-id="0c742-153">If you’re an Azure Stack operator at an organization, your users (employees) can subscribe to the services you offer without paying.</span><span class="sxs-lookup"><span data-stu-id="0c742-153">If you’re an Azure Stack operator at an organization, your users (employees) can subscribe to the services you offer without paying.</span></span>

<span data-ttu-id="0c742-154">Each combination of a user with an offer is a unique subscription.</span><span class="sxs-lookup"><span data-stu-id="0c742-154">Each combination of a user with an offer is a unique subscription.</span></span> <span data-ttu-id="0c742-155">A user can have subscriptions to multiple offers, but each subscription only applies to one offer.</span><span class="sxs-lookup"><span data-stu-id="0c742-155">A user can have subscriptions to multiple offers, but each subscription only applies to one offer.</span></span> <span data-ttu-id="0c742-156">Plans, offers, and quotas only apply to a unique subscription – they can’t be shared between subscriptions.</span><span class="sxs-lookup"><span data-stu-id="0c742-156">Plans, offers, and quotas only apply to a unique subscription – they can’t be shared between subscriptions.</span></span> <span data-ttu-id="0c742-157">Each resource that a user creates is associated with one subscription.</span><span class="sxs-lookup"><span data-stu-id="0c742-157">Each resource that a user creates is associated with one subscription.</span></span>

### <a name="default-provider-subscription"></a><span data-ttu-id="0c742-158">Default provider subscription</span><span class="sxs-lookup"><span data-stu-id="0c742-158">Default provider subscription</span></span>

<span data-ttu-id="0c742-159">The Default Provider Subscription is automatically created when you deploy the Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="0c742-159">The Default Provider Subscription is automatically created when you deploy the Azure Stack Development Kit.</span></span> <span data-ttu-id="0c742-160">This subscription can be used to manage Azure Stack, deploy additional resource providers, and create plans and offers for users.</span><span class="sxs-lookup"><span data-stu-id="0c742-160">This subscription can be used to manage Azure Stack, deploy additional resource providers, and create plans and offers for users.</span></span> <span data-ttu-id="0c742-161">For security and licensing reasons, it shouldn't be used to run customer workloads and applications.</span><span class="sxs-lookup"><span data-stu-id="0c742-161">For security and licensing reasons, it shouldn't be used to run customer workloads and applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c742-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="0c742-162">Next steps</span></span>

[<span data-ttu-id="0c742-163">Create a plan</span><span class="sxs-lookup"><span data-stu-id="0c742-163">Create a plan</span></span>](azure-stack-create-plan.md)
