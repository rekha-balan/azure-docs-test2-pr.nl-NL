---
title: Delegating offers in Azure Stack | Microsoft Docs
description: Learn how to put other people in charge of creating offers and signing up users for you.
services: azure-stack
documentationcenter: ''
author: AlfredoPizzirani
manager: byronr
editor: ''
ms.assetid: 157f0207-bddc-42e5-8351-197ec23f9d46
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: alfredop
ms.openlocfilehash: f38762f43973297b51069319513944375c1b3995
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552845"
---
# <a name="delegating-offers-in-azure-stack"></a><span data-ttu-id="e1886-103">Delegating offers in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="e1886-103">Delegating offers in Azure Stack</span></span>
<span data-ttu-id="e1886-104">As a service administrator, you often want to put other people in charge of creating offers and signing up users for you.</span><span class="sxs-lookup"><span data-stu-id="e1886-104">As a service administrator, you often want to put other people in charge of creating offers and signing up users for you.</span></span> <span data-ttu-id="e1886-105">For example, this can happen if you are a service provider and you want resellers to sign up customers and manage them on your behalf.</span><span class="sxs-lookup"><span data-stu-id="e1886-105">For example, this can happen if you are a service provider and you want resellers to sign up customers and manage them on your behalf.</span></span> <span data-ttu-id="e1886-106">It can also happen in an enterprise if you are part of a central IT group and want divisions or subsidiaries to sign up users without your intervention.</span><span class="sxs-lookup"><span data-stu-id="e1886-106">It can also happen in an enterprise if you are part of a central IT group and want divisions or subsidiaries to sign up users without your intervention.</span></span>

<span data-ttu-id="e1886-107">Delegation helps you with these tasks, helping you to reach and manage more users than you would be able to do directly.</span><span class="sxs-lookup"><span data-stu-id="e1886-107">Delegation helps you with these tasks, helping you to reach and manage more users than you would be able to do directly.</span></span> <span data-ttu-id="e1886-108">The following illustration shows one level of delegation, but Azure Stack supports multiple levels.</span><span class="sxs-lookup"><span data-stu-id="e1886-108">The following illustration shows one level of delegation, but Azure Stack supports multiple levels.</span></span> <span data-ttu-id="e1886-109">Delegated providers can in turn delegate to other providers, up to five levels.</span><span class="sxs-lookup"><span data-stu-id="e1886-109">Delegated providers can in turn delegate to other providers, up to five levels.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-delegated-provider/image1.png)

<span data-ttu-id="e1886-110">Administrators can delegate the creation of offers and tenants to other users by using the delegation functionality.</span><span class="sxs-lookup"><span data-stu-id="e1886-110">Administrators can delegate the creation of offers and tenants to other users by using the delegation functionality.</span></span>

## <a name="roles-and-steps-in-delegation"></a><span data-ttu-id="e1886-111">Roles and steps in delegation</span><span class="sxs-lookup"><span data-stu-id="e1886-111">Roles and steps in delegation</span></span>
<span data-ttu-id="e1886-112">To understand delegation, keep in mind that there are three roles involved:</span><span class="sxs-lookup"><span data-stu-id="e1886-112">To understand delegation, keep in mind that there are three roles involved:</span></span>

* <span data-ttu-id="e1886-113">The **service administrator** manages the Azure Stack infrastructure, creates an offer template, and delegates others to offer it to their users.</span><span class="sxs-lookup"><span data-stu-id="e1886-113">The **service administrator** manages the Azure Stack infrastructure, creates an offer template, and delegates others to offer it to their users.</span></span>
* <span data-ttu-id="e1886-114">The delegated users are called **delegated providers**.</span><span class="sxs-lookup"><span data-stu-id="e1886-114">The delegated users are called **delegated providers**.</span></span> <span data-ttu-id="e1886-115">They can belong to other organizations (such as other Azure Active Directory tenants).</span><span class="sxs-lookup"><span data-stu-id="e1886-115">They can belong to other organizations (such as other Azure Active Directory tenants).</span></span>
* <span data-ttu-id="e1886-116">**Users** sign up for the offers and use them for managing their workloads, creating VMs, storing data, etc.</span><span class="sxs-lookup"><span data-stu-id="e1886-116">**Users** sign up for the offers and use them for managing their workloads, creating VMs, storing data, etc.</span></span>

<span data-ttu-id="e1886-117">As shown in the following graphic, there are two steps in setting up delegation.</span><span class="sxs-lookup"><span data-stu-id="e1886-117">As shown in the following graphic, there are two steps in setting up delegation.</span></span>

1. <span data-ttu-id="e1886-118">Identify the delegated providers.</span><span class="sxs-lookup"><span data-stu-id="e1886-118">Identify the delegated providers.</span></span> <span data-ttu-id="e1886-119">Do this by subscribing them to an offer based on a plan that contains only the subscriptions service.</span><span class="sxs-lookup"><span data-stu-id="e1886-119">Do this by subscribing them to an offer based on a plan that contains only the subscriptions service.</span></span>
   <span data-ttu-id="e1886-120">Users who subscribe to this offer acquire some of the service administrator’s capabilities, including the ability to extend offers and sign users up for them.</span><span class="sxs-lookup"><span data-stu-id="e1886-120">Users who subscribe to this offer acquire some of the service administrator’s capabilities, including the ability to extend offers and sign users up for them.</span></span>
2. <span data-ttu-id="e1886-121">Delegate an offer to the delegated provider.</span><span class="sxs-lookup"><span data-stu-id="e1886-121">Delegate an offer to the delegated provider.</span></span> <span data-ttu-id="e1886-122">This offer functions as a template for what the delegated provider can offer.</span><span class="sxs-lookup"><span data-stu-id="e1886-122">This offer functions as a template for what the delegated provider can offer.</span></span> <span data-ttu-id="e1886-123">The delegated provider is now able to take the offer, choose a name for it (but not change its services and quotas), and offer it to customers.</span><span class="sxs-lookup"><span data-stu-id="e1886-123">The delegated provider is now able to take the offer, choose a name for it (but not change its services and quotas), and offer it to customers.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-delegated-provider/image2.png)

<span data-ttu-id="e1886-124">To act as delegated providers, users need to establish a relationship with the main provider; in other words, they need to create a subscription.</span><span class="sxs-lookup"><span data-stu-id="e1886-124">To act as delegated providers, users need to establish a relationship with the main provider; in other words, they need to create a subscription.</span></span> <span data-ttu-id="e1886-125">In this scenario, this subscription identifies the delegated providers as having the right to present offers on behalf of the main provider.</span><span class="sxs-lookup"><span data-stu-id="e1886-125">In this scenario, this subscription identifies the delegated providers as having the right to present offers on behalf of the main provider.</span></span>

<span data-ttu-id="e1886-126">Once this relationship is established, the system administrator can delegate an offer to the delegated provider.</span><span class="sxs-lookup"><span data-stu-id="e1886-126">Once this relationship is established, the system administrator can delegate an offer to the delegated provider.</span></span> <span data-ttu-id="e1886-127">The delegated provider is now able to take the offer, rename it (but not change its substance), and offer it to its customers.</span><span class="sxs-lookup"><span data-stu-id="e1886-127">The delegated provider is now able to take the offer, rename it (but not change its substance), and offer it to its customers.</span></span>

<span data-ttu-id="e1886-128">To establish a delegated provider, delegate an offer, and verify that users can sign up for it, carry out the instructions in the following sections.</span><span class="sxs-lookup"><span data-stu-id="e1886-128">To establish a delegated provider, delegate an offer, and verify that users can sign up for it, carry out the instructions in the following sections.</span></span>

## <a name="set-up-roles"></a><span data-ttu-id="e1886-129">Set up roles</span><span class="sxs-lookup"><span data-stu-id="e1886-129">Set up roles</span></span>
<span data-ttu-id="e1886-130">To see a delegated provider at work, you need additional Azure Active Directory accounts in addition to your service administrator account.</span><span class="sxs-lookup"><span data-stu-id="e1886-130">To see a delegated provider at work, you need additional Azure Active Directory accounts in addition to your service administrator account.</span></span> <span data-ttu-id="e1886-131">If you do not have them, create the two accounts.</span><span class="sxs-lookup"><span data-stu-id="e1886-131">If you do not have them, create the two accounts.</span></span> <span data-ttu-id="e1886-132">The accounts can belong to any AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="e1886-132">The accounts can belong to any AAD tenant.</span></span> <span data-ttu-id="e1886-133">We will refer to them as the delegated provider (DP) and the user.</span><span class="sxs-lookup"><span data-stu-id="e1886-133">We will refer to them as the delegated provider (DP) and the user.</span></span>

| <span data-ttu-id="e1886-134">**Role**</span><span class="sxs-lookup"><span data-stu-id="e1886-134">**Role**</span></span> | <span data-ttu-id="e1886-135">**Organizational rights**</span><span class="sxs-lookup"><span data-stu-id="e1886-135">**Organizational rights**</span></span> |
| --- | --- |
| <span data-ttu-id="e1886-136">Delegated Provider</span><span class="sxs-lookup"><span data-stu-id="e1886-136">Delegated Provider</span></span> |<span data-ttu-id="e1886-137">User</span><span class="sxs-lookup"><span data-stu-id="e1886-137">User</span></span> |
| <span data-ttu-id="e1886-138">User</span><span class="sxs-lookup"><span data-stu-id="e1886-138">User</span></span> |<span data-ttu-id="e1886-139">User</span><span class="sxs-lookup"><span data-stu-id="e1886-139">User</span></span> |

## <a name="identify-the-delegated-providers"></a><span data-ttu-id="e1886-140">Identify the delegated providers</span><span class="sxs-lookup"><span data-stu-id="e1886-140">Identify the delegated providers</span></span>
1. <span data-ttu-id="e1886-141">Sign in as service administrator.</span><span class="sxs-lookup"><span data-stu-id="e1886-141">Sign in as service administrator.</span></span>
2. <span data-ttu-id="e1886-142">Create the offer that will enable tenants to become delegated providers.</span><span class="sxs-lookup"><span data-stu-id="e1886-142">Create the offer that will enable tenants to become delegated providers.</span></span> <span data-ttu-id="e1886-143">This requires that you create a plan and an offer based on it:</span><span class="sxs-lookup"><span data-stu-id="e1886-143">This requires that you create a plan and an offer based on it:</span></span>
   
   <span data-ttu-id="e1886-144">a.</span><span class="sxs-lookup"><span data-stu-id="e1886-144">a.</span></span>  <span data-ttu-id="e1886-145">[Create a plan](azure-stack-create-plan.md).</span><span class="sxs-lookup"><span data-stu-id="e1886-145">[Create a plan](azure-stack-create-plan.md).</span></span>
       <span data-ttu-id="e1886-146">This plan should include only the subscriptions service.</span><span class="sxs-lookup"><span data-stu-id="e1886-146">This plan should include only the subscriptions service.</span></span> <span data-ttu-id="e1886-147">In this article, we use a plan called PlanForDelegation.</span><span class="sxs-lookup"><span data-stu-id="e1886-147">In this article, we use a plan called PlanForDelegation.</span></span>
   
   <span data-ttu-id="e1886-148">b.</span><span class="sxs-lookup"><span data-stu-id="e1886-148">b.</span></span>  <span data-ttu-id="e1886-149">[Create an offer](azure-stack-create-offer.md) based on this plan.</span><span class="sxs-lookup"><span data-stu-id="e1886-149">[Create an offer](azure-stack-create-offer.md) based on this plan.</span></span> <span data-ttu-id="e1886-150">In this article, we use an offer called OfferToDP.</span><span class="sxs-lookup"><span data-stu-id="e1886-150">In this article, we use an offer called OfferToDP.</span></span>
   
   <span data-ttu-id="e1886-151">c.</span><span class="sxs-lookup"><span data-stu-id="e1886-151">c.</span></span>  <span data-ttu-id="e1886-152">Once the creation of the offer is complete, add the delegated provider as a subscriber to this offer by clicking **Subscriptions** &gt; **Add** &gt; **New Tenant Subscription**.</span><span class="sxs-lookup"><span data-stu-id="e1886-152">Once the creation of the offer is complete, add the delegated provider as a subscriber to this offer by clicking **Subscriptions** &gt; **Add** &gt; **New Tenant Subscription**.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-delegated-provider/image3.png)

> [!NOTE]
> <span data-ttu-id="e1886-153">As with all Azure Stack offers, you have the option of making the offer public and letting users sign up for it, or keeping it private and having service administrator manage the sign-up.</span><span class="sxs-lookup"><span data-stu-id="e1886-153">As with all Azure Stack offers, you have the option of making the offer public and letting users sign up for it, or keeping it private and having service administrator manage the sign-up.</span></span> <span data-ttu-id="e1886-154">Delegated providers are usually a small group and you want to control who is admitted to it, so keeping this offer private will make sense in most cases.</span><span class="sxs-lookup"><span data-stu-id="e1886-154">Delegated providers are usually a small group and you want to control who is admitted to it, so keeping this offer private will make sense in most cases.</span></span>
> 
> 

## <a name="service-admin-creates-the-delegated-offer"></a><span data-ttu-id="e1886-155">Service admin creates the delegated offer</span><span class="sxs-lookup"><span data-stu-id="e1886-155">Service admin creates the delegated offer</span></span>
<span data-ttu-id="e1886-156">You have now established your delegated provider.</span><span class="sxs-lookup"><span data-stu-id="e1886-156">You have now established your delegated provider.</span></span> <span data-ttu-id="e1886-157">The next step is to create the plan and offer that you are going to delegate, and which your customers will use.</span><span class="sxs-lookup"><span data-stu-id="e1886-157">The next step is to create the plan and offer that you are going to delegate, and which your customers will use.</span></span> <span data-ttu-id="e1886-158">You should define this offer exactly as you want the customers to see it, because the delegated provider will not be able to change the plans and quotas it includes.</span><span class="sxs-lookup"><span data-stu-id="e1886-158">You should define this offer exactly as you want the customers to see it, because the delegated provider will not be able to change the plans and quotas it includes.</span></span>

1. <span data-ttu-id="e1886-159">As service administrator, [create a plan](azure-stack-create-plan.md) and [an offer](azure-stack-create-offer.md) based on it.</span><span class="sxs-lookup"><span data-stu-id="e1886-159">As service administrator, [create a plan](azure-stack-create-plan.md) and [an offer](azure-stack-create-offer.md) based on it.</span></span> <span data-ttu-id="e1886-160">For this article, we use an offer called DelegatedOffer.</span><span class="sxs-lookup"><span data-stu-id="e1886-160">For this article, we use an offer called DelegatedOffer.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e1886-161">This offer does not need to be made public.</span><span class="sxs-lookup"><span data-stu-id="e1886-161">This offer does not need to be made public.</span></span> <span data-ttu-id="e1886-162">It can be made public if you choose, but, in most cases, you only want delegated providers to have access to it.</span><span class="sxs-lookup"><span data-stu-id="e1886-162">It can be made public if you choose, but, in most cases, you only want delegated providers to have access to it.</span></span> <span data-ttu-id="e1886-163">Once you delegate a private offer as described in the following steps, the delegated provider will have access to it.</span><span class="sxs-lookup"><span data-stu-id="e1886-163">Once you delegate a private offer as described in the following steps, the delegated provider will have access to it.</span></span>
   > 
   > 
2. <span data-ttu-id="e1886-164">Delegate the offer.</span><span class="sxs-lookup"><span data-stu-id="e1886-164">Delegate the offer.</span></span> <span data-ttu-id="e1886-165">Go to DelegatedOffer, and in the Settings pane, click **Delegated Providers** &gt; **Add**.</span><span class="sxs-lookup"><span data-stu-id="e1886-165">Go to DelegatedOffer, and in the Settings pane, click **Delegated Providers** &gt; **Add**.</span></span>
3. <span data-ttu-id="e1886-166">Select the delegated provider’s subscription from the drop-down list box and click **Delegate**.</span><span class="sxs-lookup"><span data-stu-id="e1886-166">Select the delegated provider’s subscription from the drop-down list box and click **Delegate**.</span></span>

> ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-delegated-provider/image4.png)
> 
> 

## <a name="delegated-provider-customizes-the-offer"></a><span data-ttu-id="e1886-167">Delegated provider customizes the offer</span><span class="sxs-lookup"><span data-stu-id="e1886-167">Delegated provider customizes the offer</span></span>
<span data-ttu-id="e1886-168">Sign in as the delegated provider and create a new offer using the delegated offer as a template.</span><span class="sxs-lookup"><span data-stu-id="e1886-168">Sign in as the delegated provider and create a new offer using the delegated offer as a template.</span></span>

1. <span data-ttu-id="e1886-169">Click **New** &gt; **Tenant Offers + Plans** &gt; **Offer**.</span><span class="sxs-lookup"><span data-stu-id="e1886-169">Click **New** &gt; **Tenant Offers + Plans** &gt; **Offer**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-delegated-provider/image5.png)


1. <span data-ttu-id="e1886-170">Assign a name to the offer.</span><span class="sxs-lookup"><span data-stu-id="e1886-170">Assign a name to the offer.</span></span> <span data-ttu-id="e1886-171">Here we choose ResellerOffer.</span><span class="sxs-lookup"><span data-stu-id="e1886-171">Here we choose ResellerOffer.</span></span> <span data-ttu-id="e1886-172">Select the delegated offer to base it on and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e1886-172">Select the delegated offer to base it on and then click **Create**.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-delegated-provider/image6.png)

    >[!NOTE] 
    > <span data-ttu-id="e1886-173">Note the difference compared to offer creation as experienced by the service administrator.</span><span class="sxs-lookup"><span data-stu-id="e1886-173">Note the difference compared to offer creation as experienced by the service administrator.</span></span> <span data-ttu-id="e1886-174">The delegated provider does not           > construct the offer from base plans and add-on plans; she can only choose from offers that have been delegated to her, and will       > not make changes to them.</span><span class="sxs-lookup"><span data-stu-id="e1886-174">The delegated provider does not           > construct the offer from base plans and add-on plans; she can only choose from offers that have been delegated to her, and will       > not make changes to them.</span></span>

1. <span data-ttu-id="e1886-175">Make the offer public by clicking **Browse** &gt; **Offers**, selecting the offer, and clicking **Change State**.</span><span class="sxs-lookup"><span data-stu-id="e1886-175">Make the offer public by clicking **Browse** &gt; **Offers**, selecting the offer, and clicking **Change State**.</span></span>
2. <span data-ttu-id="e1886-176">The delegated provider exposes these offers through his or her own portal URL.</span><span class="sxs-lookup"><span data-stu-id="e1886-176">The delegated provider exposes these offers through his or her own portal URL.</span></span> <span data-ttu-id="e1886-177">Note that these offers are visible only through this    delegated portal.</span><span class="sxs-lookup"><span data-stu-id="e1886-177">Note that these offers are visible only through this    delegated portal.</span></span> <span data-ttu-id="e1886-178">To find and change this URL:</span><span class="sxs-lookup"><span data-stu-id="e1886-178">To find and change this URL:</span></span>
   
    <span data-ttu-id="e1886-179">a.</span><span class="sxs-lookup"><span data-stu-id="e1886-179">a.</span></span>  <span data-ttu-id="e1886-180">Click **Browse**&gt; **Provider Settings** &gt; **Portal URL**.</span><span class="sxs-lookup"><span data-stu-id="e1886-180">Click **Browse**&gt; **Provider Settings** &gt; **Portal URL**.</span></span>
   
    <span data-ttu-id="e1886-181">b.</span><span class="sxs-lookup"><span data-stu-id="e1886-181">b.</span></span>  <span data-ttu-id="e1886-182">Change the Provider ID if desired.</span><span class="sxs-lookup"><span data-stu-id="e1886-182">Change the Provider ID if desired.</span></span>
   
    <span data-ttu-id="e1886-183">c.</span><span class="sxs-lookup"><span data-stu-id="e1886-183">c.</span></span>  <span data-ttu-id="e1886-184">Copy the portal URL to a separate location, such as Notepad.</span><span class="sxs-lookup"><span data-stu-id="e1886-184">Copy the portal URL to a separate location, such as Notepad.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-delegated-provider/image7.png)
   
   <span data-ttu-id="e1886-185"><!-- --> You have now completed the creation of a delegated offer as a delegated provider.</span><span class="sxs-lookup"><span data-stu-id="e1886-185"><!-- --> You have now completed the creation of a delegated offer as a delegated provider.</span></span> <span data-ttu-id="e1886-186">Sign out as the delegated provider.</span><span class="sxs-lookup"><span data-stu-id="e1886-186">Sign out as the delegated provider.</span></span> <span data-ttu-id="e1886-187">Close the browser tab you have been using.</span><span class="sxs-lookup"><span data-stu-id="e1886-187">Close the browser tab you have been using.</span></span>

## <a name="sign-up-for-the-offer"></a><span data-ttu-id="e1886-188">Sign up for the offer</span><span class="sxs-lookup"><span data-stu-id="e1886-188">Sign up for the offer</span></span>
1. <span data-ttu-id="e1886-189">In a new browser window, go to the delegated portal URL you saved in the previous step.</span><span class="sxs-lookup"><span data-stu-id="e1886-189">In a new browser window, go to the delegated portal URL you saved in the previous step.</span></span> <span data-ttu-id="e1886-190">Sign in to the portal as user.</span><span class="sxs-lookup"><span data-stu-id="e1886-190">Sign in to the portal as user.</span></span> <span data-ttu-id="e1886-191">Note: you must use the delegated portal for this step.</span><span class="sxs-lookup"><span data-stu-id="e1886-191">Note: you must use the delegated portal for this step.</span></span> <span data-ttu-id="e1886-192">The delegated offer will not be visible otherwise.</span><span class="sxs-lookup"><span data-stu-id="e1886-192">The delegated offer will not be visible otherwise.</span></span>
2. <span data-ttu-id="e1886-193">In the dashboard, click **Get a subscription**.</span><span class="sxs-lookup"><span data-stu-id="e1886-193">In the dashboard, click **Get a subscription**.</span></span> <span data-ttu-id="e1886-194">You will see that only the delegated offers created by the delegated provider are presented to the user:</span><span class="sxs-lookup"><span data-stu-id="e1886-194">You will see that only the delegated offers created by the delegated provider are presented to the user:</span></span>

> ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-delegated-provider/image8.png)
> 
> 

<span data-ttu-id="e1886-195">This concludes the process of offer delegation.</span><span class="sxs-lookup"><span data-stu-id="e1886-195">This concludes the process of offer delegation.</span></span> <span data-ttu-id="e1886-196">The user can now sign up for this offer by getting a subscription for it.</span><span class="sxs-lookup"><span data-stu-id="e1886-196">The user can now sign up for this offer by getting a subscription for it.</span></span>

## <a name="multiple-tier-delegation"></a><span data-ttu-id="e1886-197">Multiple-tier delegation</span><span class="sxs-lookup"><span data-stu-id="e1886-197">Multiple-tier delegation</span></span>
<span data-ttu-id="e1886-198">Multiple-tier delegation allows the delegated provider to delegate the offer to other entities.</span><span class="sxs-lookup"><span data-stu-id="e1886-198">Multiple-tier delegation allows the delegated provider to delegate the offer to other entities.</span></span> <span data-ttu-id="e1886-199">This allows, for example, the creation of deeper reseller channels, in which the provider managing Azure Stack delegates an offer to a distributor, who in turn delegates to reseller.</span><span class="sxs-lookup"><span data-stu-id="e1886-199">This allows, for example, the creation of deeper reseller channels, in which the provider managing Azure Stack delegates an offer to a distributor, who in turn delegates to reseller.</span></span>
<span data-ttu-id="e1886-200">Azure Stack supports up to five levels of delegation.</span><span class="sxs-lookup"><span data-stu-id="e1886-200">Azure Stack supports up to five levels of delegation.</span></span>

<span data-ttu-id="e1886-201">To create multiple tiers of offer delegation, the delegated provider in turn delegates the offer to the next provider.</span><span class="sxs-lookup"><span data-stu-id="e1886-201">To create multiple tiers of offer delegation, the delegated provider in turn delegates the offer to the next provider.</span></span> <span data-ttu-id="e1886-202">The process is the same for the delegated provider as it was for the service administrator (see [Service admin creates the delegated offer](#service-admin-creates-the-delegated-offer)).</span><span class="sxs-lookup"><span data-stu-id="e1886-202">The process is the same for the delegated provider as it was for the service administrator (see [Service admin creates the delegated offer](#service-admin-creates-the-delegated-offer)).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1886-203">Next steps</span><span class="sxs-lookup"><span data-stu-id="e1886-203">Next steps</span></span>
[<span data-ttu-id="e1886-204">Provision a VM</span><span class="sxs-lookup"><span data-stu-id="e1886-204">Provision a VM</span></span>](azure-stack-provision-vm.md)









