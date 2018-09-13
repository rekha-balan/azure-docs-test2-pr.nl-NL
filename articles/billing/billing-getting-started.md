---
title: Prevent unexpected costs, manage billing - Azure | Microsoft Docs
description: Learn how to avoid unexpected charges on your Azure bill. Use cost-tracking and management features for a Microsoft Azure subscription.
services: ''
documentationcenter: ''
author: jlian
manager: mattstee
editor: ''
tags: billing
ms.assetid: 482191ac-147e-4eb6-9655-c40c13846672
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/20/2017
ms.author: jlian
ms.openlocfilehash: f24cdb75a88fe1a774b4924815f3fd0b2acfd54e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563866"
---
# <a name="prevent-unexpected-costs-with-azure-billing-and-cost-management"></a><span data-ttu-id="458c6-104">Prevent unexpected costs with Azure billing and cost management</span><span class="sxs-lookup"><span data-stu-id="458c6-104">Prevent unexpected costs with Azure billing and cost management</span></span>

<span data-ttu-id="458c6-105">When you sign up for Azure, there are several things you can do to get a better idea of your spend.</span><span class="sxs-lookup"><span data-stu-id="458c6-105">When you sign up for Azure, there are several things you can do to get a better idea of your spend.</span></span> <span data-ttu-id="458c6-106">In the [Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), when you select the subscription, you can see your current cost breakdown and burn rate.</span><span class="sxs-lookup"><span data-stu-id="458c6-106">In the [Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), when you select the subscription, you can see your current cost breakdown and burn rate.</span></span> <span data-ttu-id="458c6-107">You can also [download past invoices and detail usage files](billing-download-azure-invoice-daily-usage-date.md).</span><span class="sxs-lookup"><span data-stu-id="458c6-107">You can also [download past invoices and detail usage files](billing-download-azure-invoice-daily-usage-date.md).</span></span> <span data-ttu-id="458c6-108">If you want to group costs for resources used for different projects or teams, look at [resource tagging](../azure-resource-manager/resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="458c6-108">If you want to group costs for resources used for different projects or teams, look at [resource tagging](../azure-resource-manager/resource-group-using-tags.md).</span></span> <span data-ttu-id="458c6-109">If your organization has a reporting system that you prefer to use, check out the [billing APIs](billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="458c6-109">If your organization has a reporting system that you prefer to use, check out the [billing APIs](billing-usage-rate-card-overview.md).</span></span> 

<span data-ttu-id="458c6-110">For more information about your daily usage, see [Understand your bill for Microsoft Azure](billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="458c6-110">For more information about your daily usage, see [Understand your bill for Microsoft Azure](billing-understand-your-bill.md).</span></span>

<span data-ttu-id="458c6-111">If your subscription is through an Enterprise Agreement (EA), Cloud Solution Provider (CSP), or Azure Sponsorship, then many features in this article don't apply to you.</span><span class="sxs-lookup"><span data-stu-id="458c6-111">If your subscription is through an Enterprise Agreement (EA), Cloud Solution Provider (CSP), or Azure Sponsorship, then many features in this article don't apply to you.</span></span> <span data-ttu-id="458c6-112">Instead, we have a different set of tools that you can use for cost management.</span><span class="sxs-lookup"><span data-stu-id="458c6-112">Instead, we have a different set of tools that you can use for cost management.</span></span> <span data-ttu-id="458c6-113">See [Additional resources for EA, CSP, and Sponsorship](#other-offers).</span><span class="sxs-lookup"><span data-stu-id="458c6-113">See [Additional resources for EA, CSP, and Sponsorship](#other-offers).</span></span>

<span data-ttu-id="458c6-114">If your subscription is a Free Trial, [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), Azure in Open (AIO), or BizSpark, then learn about [spending limits](#spending-limit) to avoid having your subscription unexpectantly disabled.</span><span class="sxs-lookup"><span data-stu-id="458c6-114">If your subscription is a Free Trial, [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), Azure in Open (AIO), or BizSpark, then learn about [spending limits](#spending-limit) to avoid having your subscription unexpectantly disabled.</span></span> 

## <a name="day-0-before-you-add-azure-services"></a><span data-ttu-id="458c6-115">Day 0: Before you add Azure services</span><span class="sxs-lookup"><span data-stu-id="458c6-115">Day 0: Before you add Azure services</span></span>

### <a name="estimate-cost-online-using-the-pricing-calculator"></a><span data-ttu-id="458c6-116">Estimate cost online using the pricing calculator</span><span class="sxs-lookup"><span data-stu-id="458c6-116">Estimate cost online using the pricing calculator</span></span>

<span data-ttu-id="458c6-117">Check out the [pricing calculator](https://azure.microsoft.com/pricing/calculator/) and [total cost of ownership calculator](https://aka.ms/azure-tco-calculator) to get an estimate the monthly cost of the service you're interested in.</span><span class="sxs-lookup"><span data-stu-id="458c6-117">Check out the [pricing calculator](https://azure.microsoft.com/pricing/calculator/) and [total cost of ownership calculator](https://aka.ms/azure-tco-calculator) to get an estimate the monthly cost of the service you're interested in.</span></span> <span data-ttu-id="458c6-118">For example, an A1 Windows Virtual Machine (VM) is estimated to cost $66.96 USD/month in compute hours if you leave it running the whole time:</span><span class="sxs-lookup"><span data-stu-id="458c6-118">For example, an A1 Windows Virtual Machine (VM) is estimated to cost $66.96 USD/month in compute hours if you leave it running the whole time:</span></span>

![Screenshot of the pricing calculator showing that an A1 Windows VM is estimated to cost $66.96 USD per month](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-getting-started/pricing-calc.PNG)

<span data-ttu-id="458c6-120">For more information, see [pricing FAQ](https://azure.microsoft.com/pricing/faq/).</span><span class="sxs-lookup"><span data-stu-id="458c6-120">For more information, see [pricing FAQ](https://azure.microsoft.com/pricing/faq/).</span></span> <span data-ttu-id="458c6-121">Or if you want to talk to a person, call 1-800-867-1389.</span><span class="sxs-lookup"><span data-stu-id="458c6-121">Or if you want to talk to a person, call 1-800-867-1389.</span></span>

### <a name="check-your-subscription-and-access"></a><span data-ttu-id="458c6-122">Check your subscription and access</span><span class="sxs-lookup"><span data-stu-id="458c6-122">Check your subscription and access</span></span>

<span data-ttu-id="458c6-123">Viewing costs require [subscriptions-level access](../active-directory/role-based-access-control-configure.md), but only the Account admin can access the [Account Center](https://account.windowsazure.com/Home/Index), change billing info, and manage subscriptions.</span><span class="sxs-lookup"><span data-stu-id="458c6-123">Viewing costs require [subscriptions-level access](../active-directory/role-based-access-control-configure.md), but only the Account admin can access the [Account Center](https://account.windowsazure.com/Home/Index), change billing info, and manage subscriptions.</span></span> <span data-ttu-id="458c6-124">The Account admin is the person who went through the sign-up process.</span><span class="sxs-lookup"><span data-stu-id="458c6-124">The Account admin is the person who went through the sign-up process.</span></span> <span data-ttu-id="458c6-125">For more information, see [How to add or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="458c6-125">For more information, see [How to add or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="458c6-126">To see if you're the Account admin, go to the [Subscriptions blade in the Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) and look at the list of subscriptions you have access to.</span><span class="sxs-lookup"><span data-stu-id="458c6-126">To see if you're the Account admin, go to the [Subscriptions blade in the Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) and look at the list of subscriptions you have access to.</span></span> <span data-ttu-id="458c6-127">Look under **My Role**.</span><span class="sxs-lookup"><span data-stu-id="458c6-127">Look under **My Role**.</span></span> <span data-ttu-id="458c6-128">If it says *Account admin*, then you're ok.</span><span class="sxs-lookup"><span data-stu-id="458c6-128">If it says *Account admin*, then you're ok.</span></span> <span data-ttu-id="458c6-129">If it says something else like *Owner*, then you don't have full privileges.</span><span class="sxs-lookup"><span data-stu-id="458c6-129">If it says something else like *Owner*, then you don't have full privileges.</span></span>

![Screenshot of your role in the Subscriptions view in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-getting-started/sub-blade-view.PNG)

<span data-ttu-id="458c6-131">If you're not the Account admin, then somebody probably gave you partial access via [Azure Active Directory Role-based Access Control](../active-directory/role-based-access-control-configure.md) (RBAC).</span><span class="sxs-lookup"><span data-stu-id="458c6-131">If you're not the Account admin, then somebody probably gave you partial access via [Azure Active Directory Role-based Access Control](../active-directory/role-based-access-control-configure.md) (RBAC).</span></span> <span data-ttu-id="458c6-132">To manage subscriptions and change billing info, [find the Account admin](billing-subscription-transfer.md#whoisaa) and ask them to perform the tasks or [transfer the subscription to you](billing-subscription-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="458c6-132">To manage subscriptions and change billing info, [find the Account admin](billing-subscription-transfer.md#whoisaa) and ask them to perform the tasks or [transfer the subscription to you](billing-subscription-transfer.md).</span></span>

<span data-ttu-id="458c6-133">If your Account admin is no longer with your organization and you need to manage billing, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="458c6-133">If your Account admin is no longer with your organization and you need to manage billing, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> 

### <a name="spending-limit"></a> <span data-ttu-id="458c6-134">Check if you have a spending limit on</span><span class="sxs-lookup"><span data-stu-id="458c6-134">Check if you have a spending limit on</span></span>

<span data-ttu-id="458c6-135">If you have a subscription that uses credits, then the spending limit is turned on for you by default.</span><span class="sxs-lookup"><span data-stu-id="458c6-135">If you have a subscription that uses credits, then the spending limit is turned on for you by default.</span></span> <span data-ttu-id="458c6-136">This way, when you spend all your credits, your credit card doesn't get charged.</span><span class="sxs-lookup"><span data-stu-id="458c6-136">This way, when you spend all your credits, your credit card doesn't get charged.</span></span> <span data-ttu-id="458c6-137">See the [full list of Azure offers and the availability of spending limit](https://azure.microsoft.com/support/legal/offer-details/).</span><span class="sxs-lookup"><span data-stu-id="458c6-137">See the [full list of Azure offers and the availability of spending limit](https://azure.microsoft.com/support/legal/offer-details/).</span></span>

<span data-ttu-id="458c6-138">However, if you hit your spending limit, your services get disabled.</span><span class="sxs-lookup"><span data-stu-id="458c6-138">However, if you hit your spending limit, your services get disabled.</span></span> <span data-ttu-id="458c6-139">That means your VMs are deallocated.</span><span class="sxs-lookup"><span data-stu-id="458c6-139">That means your VMs are deallocated.</span></span> <span data-ttu-id="458c6-140">To avoid service downtime, you must turn off the spending limit.</span><span class="sxs-lookup"><span data-stu-id="458c6-140">To avoid service downtime, you must turn off the spending limit.</span></span> <span data-ttu-id="458c6-141">Any overage gets charged onto your credit card on file.</span><span class="sxs-lookup"><span data-stu-id="458c6-141">Any overage gets charged onto your credit card on file.</span></span> 

<span data-ttu-id="458c6-142">To see if you've got spending limit on, go to the [Subscriptions view in the Account Center](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="458c6-142">To see if you've got spending limit on, go to the [Subscriptions view in the Account Center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="458c6-143">A banner appears if your spending limit is on:</span><span class="sxs-lookup"><span data-stu-id="458c6-143">A banner appears if your spending limit is on:</span></span>

![Screenshot that shows a warning about spending limit being on in the Account Center](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-getting-started/spending-limit-banner.PNG)

<span data-ttu-id="458c6-145">Click the banner and follow prompts to remove the spending limit.</span><span class="sxs-lookup"><span data-stu-id="458c6-145">Click the banner and follow prompts to remove the spending limit.</span></span> <span data-ttu-id="458c6-146">If you didn't enter credit card information when you signed up, you must enter it to remove the spending limit.</span><span class="sxs-lookup"><span data-stu-id="458c6-146">If you didn't enter credit card information when you signed up, you must enter it to remove the spending limit.</span></span> <span data-ttu-id="458c6-147">For more information, see [Azure spending limit – How it works and how to enable or remove it](https://azure.microsoft.com/pricing/spending-limits/).</span><span class="sxs-lookup"><span data-stu-id="458c6-147">For more information, see [Azure spending limit – How it works and how to enable or remove it](https://azure.microsoft.com/pricing/spending-limits/).</span></span>

### <a name="set-up-billing-alerts"></a><span data-ttu-id="458c6-148">Set up billing alerts</span><span class="sxs-lookup"><span data-stu-id="458c6-148">Set up billing alerts</span></span>

<span data-ttu-id="458c6-149">Set up billing alerts to get emails when your usage costs exceed an amount that you specify.</span><span class="sxs-lookup"><span data-stu-id="458c6-149">Set up billing alerts to get emails when your usage costs exceed an amount that you specify.</span></span> <span data-ttu-id="458c6-150">If you have monthly credits, set up alerts for when you use up a specified amount.</span><span class="sxs-lookup"><span data-stu-id="458c6-150">If you have monthly credits, set up alerts for when you use up a specified amount.</span></span> <span data-ttu-id="458c6-151">For more information, see [Set up billing alerts for your Microsoft Azure subscriptions](billing-set-up-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="458c6-151">For more information, see [Set up billing alerts for your Microsoft Azure subscriptions](billing-set-up-alerts.md).</span></span>

![Screenshot of a billing alert email](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-getting-started/billing-alert.png)

> [!NOTE]
> <span data-ttu-id="458c6-153">This feature is still in preview so you should check your usage regularly.</span><span class="sxs-lookup"><span data-stu-id="458c6-153">This feature is still in preview so you should check your usage regularly.</span></span>

<span data-ttu-id="458c6-154">You might want to use the cost estimate from the pricing calculator as a guideline for your first alert.</span><span class="sxs-lookup"><span data-stu-id="458c6-154">You might want to use the cost estimate from the pricing calculator as a guideline for your first alert.</span></span>

### <a name="understand-limits-and-quotas-for-your-subscription"></a><span data-ttu-id="458c6-155">Understand limits and quotas for your subscription</span><span class="sxs-lookup"><span data-stu-id="458c6-155">Understand limits and quotas for your subscription</span></span>

<span data-ttu-id="458c6-156">There are default limits to each subscription for things like the number of CPU cores and IP addresses.</span><span class="sxs-lookup"><span data-stu-id="458c6-156">There are default limits to each subscription for things like the number of CPU cores and IP addresses.</span></span> <span data-ttu-id="458c6-157">Be mindful of these limits.</span><span class="sxs-lookup"><span data-stu-id="458c6-157">Be mindful of these limits.</span></span> <span data-ttu-id="458c6-158">For more information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="458c6-158">For more information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="458c6-159">You can request an increase to your limit or quota by [contacting support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="458c6-159">You can request an increase to your limit or quota by [contacting support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="day-1-as-you-add-services"></a><span data-ttu-id="458c6-160">Day 1: As you add services</span><span class="sxs-lookup"><span data-stu-id="458c6-160">Day 1: As you add services</span></span>

### <a name="review-the-estimated-cost-in-the-portal"></a><span data-ttu-id="458c6-161">Review the estimated cost in the portal</span><span class="sxs-lookup"><span data-stu-id="458c6-161">Review the estimated cost in the portal</span></span>

<span data-ttu-id="458c6-162">Typically when you add a service in the Azure portal, there's a view that shows you a similar estimated cost per month.</span><span class="sxs-lookup"><span data-stu-id="458c6-162">Typically when you add a service in the Azure portal, there's a view that shows you a similar estimated cost per month.</span></span> <span data-ttu-id="458c6-163">For example, when you choose the size of your Windows VM you see the estimated monthly cost for the compute hours:</span><span class="sxs-lookup"><span data-stu-id="458c6-163">For example, when you choose the size of your Windows VM you see the estimated monthly cost for the compute hours:</span></span>

![Example: an A1 Windows VM is estimated to cost $66.96 USD per month](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-getting-started/vm-size-cost.PNG)

### <a name="tags"></a> <span data-ttu-id="458c6-165">Add tags to your resources to group your billing data</span><span class="sxs-lookup"><span data-stu-id="458c6-165">Add tags to your resources to group your billing data</span></span>

<span data-ttu-id="458c6-166">You can use tags to group billing data for supported services.</span><span class="sxs-lookup"><span data-stu-id="458c6-166">You can use tags to group billing data for supported services.</span></span> <span data-ttu-id="458c6-167">For example, if you run several VMs for different teams, then you can use tags to categorize costs by cost center (HR, marketing, finance) or environment (production, pre-production, test).</span><span class="sxs-lookup"><span data-stu-id="458c6-167">For example, if you run several VMs for different teams, then you can use tags to categorize costs by cost center (HR, marketing, finance) or environment (production, pre-production, test).</span></span> 

![Screenshot that shows setting up tags in the portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-getting-started/tags.PNG)

<span data-ttu-id="458c6-169">The tags show up throughout different cost reporting views.</span><span class="sxs-lookup"><span data-stu-id="458c6-169">The tags show up throughout different cost reporting views.</span></span> <span data-ttu-id="458c6-170">For example, they're visible in your [cost analysis view](#costs) right away and [detail usage .csv](#invoice-and-usage) after your first billing period.</span><span class="sxs-lookup"><span data-stu-id="458c6-170">For example, they're visible in your [cost analysis view](#costs) right away and [detail usage .csv](#invoice-and-usage) after your first billing period.</span></span>

<span data-ttu-id="458c6-171">For more information, see [Using tags to organize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="458c6-171">For more information, see [Using tags to organize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>

### <a name="consider-enabling-cost-cutting-features-like-auto-shutdown-for-vms"></a><span data-ttu-id="458c6-172">Consider enabling cost-cutting features like auto-shutdown for VMs</span><span class="sxs-lookup"><span data-stu-id="458c6-172">Consider enabling cost-cutting features like auto-shutdown for VMs</span></span>

<span data-ttu-id="458c6-173">Depending on your scenario, you could configure auto-shutdown for your VMs in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="458c6-173">Depending on your scenario, you could configure auto-shutdown for your VMs in the Azure portal.</span></span> <span data-ttu-id="458c6-174">For more information, see [Auto-shutdown for VMs using Azure Resource Manager](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).</span><span class="sxs-lookup"><span data-stu-id="458c6-174">For more information, see [Auto-shutdown for VMs using Azure Resource Manager](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).</span></span>

![Screenshot of auto-shutdown option in the portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-getting-started/auto-shutdown.PNG)

<span data-ttu-id="458c6-176">Auto-shutdown isn't the same as when you shut down within the VM with power options.</span><span class="sxs-lookup"><span data-stu-id="458c6-176">Auto-shutdown isn't the same as when you shut down within the VM with power options.</span></span> <span data-ttu-id="458c6-177">Auto-shutdown stops and deallocates your VMs to stop additional usage charges.</span><span class="sxs-lookup"><span data-stu-id="458c6-177">Auto-shutdown stops and deallocates your VMs to stop additional usage charges.</span></span> <span data-ttu-id="458c6-178">For more information, see pricing FAQ for [Linux VMs](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) and [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) about VM states.</span><span class="sxs-lookup"><span data-stu-id="458c6-178">For more information, see pricing FAQ for [Linux VMs](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) and [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) about VM states.</span></span>

<span data-ttu-id="458c6-179">For more cost-cutting features for your development and test environments, check out [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/).</span><span class="sxs-lookup"><span data-stu-id="458c6-179">For more cost-cutting features for your development and test environments, check out [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/).</span></span>

## <a name="cost-reporting"></a> <span data-ttu-id="458c6-180">Day 2+: After using services, view usage</span><span class="sxs-lookup"><span data-stu-id="458c6-180">Day 2+: After using services, view usage</span></span>

### <a name="costs"></a> <span data-ttu-id="458c6-181">Regularly check the portal for cost breakdown and burn rate</span><span class="sxs-lookup"><span data-stu-id="458c6-181">Regularly check the portal for cost breakdown and burn rate</span></span>

<span data-ttu-id="458c6-182">After you get your services running, regularly check how much they're costing you.</span><span class="sxs-lookup"><span data-stu-id="458c6-182">After you get your services running, regularly check how much they're costing you.</span></span> <span data-ttu-id="458c6-183">You can see the current spend and burn rate in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="458c6-183">You can see the current spend and burn rate in Azure portal.</span></span> 

1. <span data-ttu-id="458c6-184">Visit the [Subscriptions blade in Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span><span class="sxs-lookup"><span data-stu-id="458c6-184">Visit the [Subscriptions blade in Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span></span>

2. <span data-ttu-id="458c6-185">Select your subscription you want to see.</span><span class="sxs-lookup"><span data-stu-id="458c6-185">Select your subscription you want to see.</span></span> <span data-ttu-id="458c6-186">You might only have one to select.</span><span class="sxs-lookup"><span data-stu-id="458c6-186">You might only have one to select.</span></span>

3. <span data-ttu-id="458c6-187">You should see the cost breakdown and burn rate in the popup blade.</span><span class="sxs-lookup"><span data-stu-id="458c6-187">You should see the cost breakdown and burn rate in the popup blade.</span></span> <span data-ttu-id="458c6-188">It may not be supported for your offer (a warning would be displayed near the top).</span><span class="sxs-lookup"><span data-stu-id="458c6-188">It may not be supported for your offer (a warning would be displayed near the top).</span></span> <span data-ttu-id="458c6-189">Wait 24 hours after you add a service for the data to populate.</span><span class="sxs-lookup"><span data-stu-id="458c6-189">Wait 24 hours after you add a service for the data to populate.</span></span>
    
    ![Screenshot of burn rate and breakdown in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-getting-started/burn-rate.PNG)

4. <span data-ttu-id="458c6-191">You might want to pin the view to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="458c6-191">You might want to pin the view to your dashboard.</span></span>

    ![Screenshot of pinning a view to the dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-getting-started/pin.png)

5. <span data-ttu-id="458c6-193">Click **Cost analysis** in the list to the left to see the cost breakdown by resource.</span><span class="sxs-lookup"><span data-stu-id="458c6-193">Click **Cost analysis** in the list to the left to see the cost breakdown by resource.</span></span>

    ![Screenshot of the cost analysis view in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-getting-started/cost-analysis.PNG)

6. <span data-ttu-id="458c6-195">You can filter by different properties like [tags](#tags), resource group, and timespan.</span><span class="sxs-lookup"><span data-stu-id="458c6-195">You can filter by different properties like [tags](#tags), resource group, and timespan.</span></span> <span data-ttu-id="458c6-196">Click **Apply** to confirm the filters and **Download** to export the view to a Comma-Separated Values (.csv) file.</span><span class="sxs-lookup"><span data-stu-id="458c6-196">Click **Apply** to confirm the filters and **Download** to export the view to a Comma-Separated Values (.csv) file.</span></span>

7. <span data-ttu-id="458c6-197">Click a resource to see spend history and how much it was costing you each day.</span><span class="sxs-lookup"><span data-stu-id="458c6-197">Click a resource to see spend history and how much it was costing you each day.</span></span>

    ![Screenshot of the spend history view in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-getting-started/spend-history.PNG)

<span data-ttu-id="458c6-199">We recommend that you check the costs you see with the estimates you saw when you selected the services.</span><span class="sxs-lookup"><span data-stu-id="458c6-199">We recommend that you check the costs you see with the estimates you saw when you selected the services.</span></span> <span data-ttu-id="458c6-200">If the costs wildly differ from estimates, double check the pricing plan (A1 vs A0 VM, for example) that you've selected for your resources.</span><span class="sxs-lookup"><span data-stu-id="458c6-200">If the costs wildly differ from estimates, double check the pricing plan (A1 vs A0 VM, for example) that you've selected for your resources.</span></span> 

#### <a name="view-costs-for-all-your-subscriptions-in-the-billing-blade"></a><span data-ttu-id="458c6-201">View costs for all your subscriptions in the Billing blade</span><span class="sxs-lookup"><span data-stu-id="458c6-201">View costs for all your subscriptions in the Billing blade</span></span>

<span data-ttu-id="458c6-202">If you manage multiple subscriptions as the Account admin, you can see the aggregate bill amount and breakdown for all your subscriptions in the [Billing blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade).</span><span class="sxs-lookup"><span data-stu-id="458c6-202">If you manage multiple subscriptions as the Account admin, you can see the aggregate bill amount and breakdown for all your subscriptions in the [Billing blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade).</span></span> 

<!-- Add screenshots of multiple subs each with billed usage -->

### <a name="turn-on-and-check-out-azure-advisor-recommendations"></a><span data-ttu-id="458c6-203">Turn on and check out Azure Advisor recommendations</span><span class="sxs-lookup"><span data-stu-id="458c6-203">Turn on and check out Azure Advisor recommendations</span></span>

<span data-ttu-id="458c6-204">[Azure Advisor](../advisor/advisor-overview.md) is a preview feature that helps you reduce costs by identifying resources with low usage.</span><span class="sxs-lookup"><span data-stu-id="458c6-204">[Azure Advisor](../advisor/advisor-overview.md) is a preview feature that helps you reduce costs by identifying resources with low usage.</span></span> <span data-ttu-id="458c6-205">Turn it on in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="458c6-205">Turn it on in the Azure portal:</span></span>

![Screenshot of Azure Advisor button in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-getting-started/advisor-button.PNG)

<span data-ttu-id="458c6-207">Then, you can get actionable recommendations in the **Cost** tab in the Advisor dashboard:</span><span class="sxs-lookup"><span data-stu-id="458c6-207">Then, you can get actionable recommendations in the **Cost** tab in the Advisor dashboard:</span></span>

![Screenshot of Advisor cost recommendation example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-getting-started/advisor-action.PNG)

<span data-ttu-id="458c6-209">For more information, see [Advisor Cost recommendations](../advisor/advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="458c6-209">For more information, see [Advisor Cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

### <a name="invoice-and-usage"></a> <span data-ttu-id="458c6-210">Get your invoice and detail usage after your first billing period</span><span class="sxs-lookup"><span data-stu-id="458c6-210">Get your invoice and detail usage after your first billing period</span></span>

<span data-ttu-id="458c6-211">After your first billing period, you can download your Portable Document Format (.pdf) invoice and Comma-Separated Values (.csv) usage details.</span><span class="sxs-lookup"><span data-stu-id="458c6-211">After your first billing period, you can download your Portable Document Format (.pdf) invoice and Comma-Separated Values (.csv) usage details.</span></span> <span data-ttu-id="458c6-212">You can also opt in to have your invoice emailed to you.</span><span class="sxs-lookup"><span data-stu-id="458c6-212">You can also opt in to have your invoice emailed to you.</span></span> <span data-ttu-id="458c6-213">These files help to understand what is ultimately billed to you after tax, discounts, and credits.</span><span class="sxs-lookup"><span data-stu-id="458c6-213">These files help to understand what is ultimately billed to you after tax, discounts, and credits.</span></span> <span data-ttu-id="458c6-214">If you didn't have a payment method attached to your subscription, these files might be unavailable for you.</span><span class="sxs-lookup"><span data-stu-id="458c6-214">If you didn't have a payment method attached to your subscription, these files might be unavailable for you.</span></span> <span data-ttu-id="458c6-215">For more information, see [How to get your Azure billing invoice and daily usage data](billing-download-azure-invoice-daily-usage-date.md) and [Understand your bill for Microsoft Azure](billing-understand-your-bill.md).</span><span class="sxs-lookup"><span data-stu-id="458c6-215">For more information, see [How to get your Azure billing invoice and daily usage data](billing-download-azure-invoice-daily-usage-date.md) and [Understand your bill for Microsoft Azure](billing-understand-your-bill.md).</span></span>

![Screenshot of a .pdf invoice](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-getting-started/invoice.png)

<span data-ttu-id="458c6-217">The tags that you set earlier show up in the detail usage .csv files:</span><span class="sxs-lookup"><span data-stu-id="458c6-217">The tags that you set earlier show up in the detail usage .csv files:</span></span>

![Screenshot that shows tags in the usage .csv](https://docstestmedia1.blob.core.windows.net/azure-media/articles/billing/media/billing-getting-started/csv.png)

### <a name="billing-api"></a><span data-ttu-id="458c6-219">Billing API</span><span class="sxs-lookup"><span data-stu-id="458c6-219">Billing API</span></span>

<span data-ttu-id="458c6-220">Use our billing API to programmatically get usage data.</span><span class="sxs-lookup"><span data-stu-id="458c6-220">Use our billing API to programmatically get usage data.</span></span> <span data-ttu-id="458c6-221">Use the RateCard API and the Usage API together to get your billed usage.</span><span class="sxs-lookup"><span data-stu-id="458c6-221">Use the RateCard API and the Usage API together to get your billed usage.</span></span> <span data-ttu-id="458c6-222">For more information, see [Gain insights into your Microsoft Azure resource consumption](billing-usage-rate-card-overview.md).</span><span class="sxs-lookup"><span data-stu-id="458c6-222">For more information, see [Gain insights into your Microsoft Azure resource consumption](billing-usage-rate-card-overview.md).</span></span>

## <a name="other-offers"></a> <span data-ttu-id="458c6-223">Additional resources for EA, CSP, and Sponsorship</span><span class="sxs-lookup"><span data-stu-id="458c6-223">Additional resources for EA, CSP, and Sponsorship</span></span>

<span data-ttu-id="458c6-224">Talk to your account manager or Azure partner to get started.</span><span class="sxs-lookup"><span data-stu-id="458c6-224">Talk to your account manager or Azure partner to get started.</span></span>

| <span data-ttu-id="458c6-225">Offer</span><span class="sxs-lookup"><span data-stu-id="458c6-225">Offer</span></span> | <span data-ttu-id="458c6-226">Resources</span><span class="sxs-lookup"><span data-stu-id="458c6-226">Resources</span></span> |
|-------------------------------|-----------------------------------------------------------------------------------|
| <span data-ttu-id="458c6-227">Enterprise Agreement (EA)</span><span class="sxs-lookup"><span data-stu-id="458c6-227">Enterprise Agreement (EA)</span></span> | <span data-ttu-id="458c6-228">[EA portal](https://ea.azure.com/), [help docs](https://ea.azure.com/helpdocs), and [Power BI report](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/)</span><span class="sxs-lookup"><span data-stu-id="458c6-228">[EA portal](https://ea.azure.com/), [help docs](https://ea.azure.com/helpdocs), and [Power BI report](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/)</span></span> |
| <span data-ttu-id="458c6-229">Cloud Solution Provider (CSP)</span><span class="sxs-lookup"><span data-stu-id="458c6-229">Cloud Solution Provider (CSP)</span></span> | <span data-ttu-id="458c6-230">Talk to your provider</span><span class="sxs-lookup"><span data-stu-id="458c6-230">Talk to your provider</span></span> |
| <span data-ttu-id="458c6-231">Azure Sponsorship</span><span class="sxs-lookup"><span data-stu-id="458c6-231">Azure Sponsorship</span></span> | [<span data-ttu-id="458c6-232">Sponsorship portal</span><span class="sxs-lookup"><span data-stu-id="458c6-232">Sponsorship portal</span></span>](https://www.microsoftazuresponsorships.com/) |

<span data-ttu-id="458c6-233">If you're managing IT for a large organization, we recommend reading [Azure enterprise scaffold](../azure-resource-manager/resource-manager-subscription-governance.md) and the [enterprise IT white paper](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (.pdf download, English only).</span><span class="sxs-lookup"><span data-stu-id="458c6-233">If you're managing IT for a large organization, we recommend reading [Azure enterprise scaffold](../azure-resource-manager/resource-manager-subscription-governance.md) and the [enterprise IT white paper](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (.pdf download, English only).</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="458c6-234">Need help?</span><span class="sxs-lookup"><span data-stu-id="458c6-234">Need help?</span></span> <span data-ttu-id="458c6-235">Contact support</span><span class="sxs-lookup"><span data-stu-id="458c6-235">Contact support</span></span>

<span data-ttu-id="458c6-236">If you need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span><span class="sxs-lookup"><span data-stu-id="458c6-236">If you need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>














