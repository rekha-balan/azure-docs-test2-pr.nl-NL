---
title: Make virtual machines available to your Azure Stack users| Microsoft Docs
description: Learn how to make virtual machines available on Azure Stack
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 09/05/2018
ms.author: jeffgilb
ms.reviewer: ''
ms.custom: mvc
ms.openlocfilehash: 09b9126125006fb70f5e2560f04b815b4a874405
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870930"
---
# <a name="tutorial-make-virtual-machines-available-to-your-azure-stack-users"></a><span data-ttu-id="daeb5-103">Tutorial: make virtual machines available to your Azure Stack users</span><span class="sxs-lookup"><span data-stu-id="daeb5-103">Tutorial: make virtual machines available to your Azure Stack users</span></span>

<span data-ttu-id="daeb5-104">As an Azure Stack cloud administrator, you can create offers that your users (sometimes referred to as tenants) can subscribe to.</span><span class="sxs-lookup"><span data-stu-id="daeb5-104">As an Azure Stack cloud administrator, you can create offers that your users (sometimes referred to as tenants) can subscribe to.</span></span> <span data-ttu-id="daeb5-105">By subscribing to an offer, users can consume the Azure Stack services that an offer provides.</span><span class="sxs-lookup"><span data-stu-id="daeb5-105">By subscribing to an offer, users can consume the Azure Stack services that an offer provides.</span></span>

<span data-ttu-id="daeb5-106">This tutorial shows how to create an offer for a virtual machine, and then sign in as a user to test the offer.</span><span class="sxs-lookup"><span data-stu-id="daeb5-106">This tutorial shows how to create an offer for a virtual machine, and then sign in as a user to test the offer.</span></span>

<span data-ttu-id="daeb5-107">What you will learn:</span><span class="sxs-lookup"><span data-stu-id="daeb5-107">What you will learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="daeb5-108">Create an offer</span><span class="sxs-lookup"><span data-stu-id="daeb5-108">Create an offer</span></span>
> * <span data-ttu-id="daeb5-109">Add an image</span><span class="sxs-lookup"><span data-stu-id="daeb5-109">Add an image</span></span>
> * <span data-ttu-id="daeb5-110">Test the offer</span><span class="sxs-lookup"><span data-stu-id="daeb5-110">Test the offer</span></span>

<span data-ttu-id="daeb5-111">In Azure Stack, services are delivered to users using subscriptions, offers, and plans.</span><span class="sxs-lookup"><span data-stu-id="daeb5-111">In Azure Stack, services are delivered to users using subscriptions, offers, and plans.</span></span> <span data-ttu-id="daeb5-112">Users can subscribe to multiple offers.</span><span class="sxs-lookup"><span data-stu-id="daeb5-112">Users can subscribe to multiple offers.</span></span> <span data-ttu-id="daeb5-113">An offer can have one or more plans, and a plan can have one or more services.</span><span class="sxs-lookup"><span data-stu-id="daeb5-113">An offer can have one or more plans, and a plan can have one or more services.</span></span>

![Subscriptions, offers, and plans](media/azure-stack-key-features/image4.png)

<span data-ttu-id="daeb5-115">To learn more, see [Key features and concepts in Azure Stack](azure-stack-key-features.md).</span><span class="sxs-lookup"><span data-stu-id="daeb5-115">To learn more, see [Key features and concepts in Azure Stack](azure-stack-key-features.md).</span></span>

## <a name="create-an-offer"></a><span data-ttu-id="daeb5-116">Create an offer</span><span class="sxs-lookup"><span data-stu-id="daeb5-116">Create an offer</span></span>

<span data-ttu-id="daeb5-117">Offers are groups of one or more plans that providers present to users to purchase or subscribe to.</span><span class="sxs-lookup"><span data-stu-id="daeb5-117">Offers are groups of one or more plans that providers present to users to purchase or subscribe to.</span></span> <span data-ttu-id="daeb5-118">The process of creating an offer has several steps.</span><span class="sxs-lookup"><span data-stu-id="daeb5-118">The process of creating an offer has several steps.</span></span> <span data-ttu-id="daeb5-119">First, you're prompted to create the offer, then a plan, and finally, quotas.</span><span class="sxs-lookup"><span data-stu-id="daeb5-119">First, you're prompted to create the offer, then a plan, and finally, quotas.</span></span>

1. <span data-ttu-id="daeb5-120">[Sign in](azure-stack-connect-azure-stack.md) to the portal as a cloud administrator and then select **New** > **Offers + Plans** > **Offer**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-120">[Sign in](azure-stack-connect-azure-stack.md) to the portal as a cloud administrator and then select **New** > **Offers + Plans** > **Offer**.</span></span>

   ![New offer](media/azure-stack-tutorial-tenant-vm/image01.png)

1. <span data-ttu-id="daeb5-122">In **New Offer**, enter a **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-122">In **New Offer**, enter a **Display Name** and **Resource Name**, and then select a new or existing **Resource Group**.</span></span> <span data-ttu-id="daeb5-123">The Display Name is the offer's friendly name.</span><span class="sxs-lookup"><span data-stu-id="daeb5-123">The Display Name is the offer's friendly name.</span></span> <span data-ttu-id="daeb5-124">Only the cloud operator can see the Resource Name.</span><span class="sxs-lookup"><span data-stu-id="daeb5-124">Only the cloud operator can see the Resource Name.</span></span> <span data-ttu-id="daeb5-125">It's the name that admins use to work with the offer as an Azure Resource Manager resource.</span><span class="sxs-lookup"><span data-stu-id="daeb5-125">It's the name that admins use to work with the offer as an Azure Resource Manager resource.</span></span>

   ![Display name](media/azure-stack-tutorial-tenant-vm/image02.png)

1. <span data-ttu-id="daeb5-127">Select **Base plans**, and in the **Plan** section, select **Add** to add a new plan to the offer.</span><span class="sxs-lookup"><span data-stu-id="daeb5-127">Select **Base plans**, and in the **Plan** section, select **Add** to add a new plan to the offer.</span></span>

   ![Add a plan](media/azure-stack-tutorial-tenant-vm/image03.png)

1. <span data-ttu-id="daeb5-129">In the **New Plan** section, fill in **Display Name** and **Resource Name**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-129">In the **New Plan** section, fill in **Display Name** and **Resource Name**.</span></span> <span data-ttu-id="daeb5-130">The Display Name is the plan's friendly name that users see.</span><span class="sxs-lookup"><span data-stu-id="daeb5-130">The Display Name is the plan's friendly name that users see.</span></span> <span data-ttu-id="daeb5-131">Only the cloud operator can see the Resource Name.</span><span class="sxs-lookup"><span data-stu-id="daeb5-131">Only the cloud operator can see the Resource Name.</span></span> <span data-ttu-id="daeb5-132">It's the name that cloud operators use to work with the plan as an Azure Resource Manager resource.</span><span class="sxs-lookup"><span data-stu-id="daeb5-132">It's the name that cloud operators use to work with the plan as an Azure Resource Manager resource.</span></span>

   ![Plan display name](media/azure-stack-tutorial-tenant-vm/image04.png)

1. <span data-ttu-id="daeb5-134">Select **Services**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-134">Select **Services**.</span></span> <span data-ttu-id="daeb5-135">From the list of Services, pick  **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-135">From the list of Services, pick  **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**.</span></span> <span data-ttu-id="daeb5-136">Choose **Select** to add these services to the plan.</span><span class="sxs-lookup"><span data-stu-id="daeb5-136">Choose **Select** to add these services to the plan.</span></span>

   ![Plan services](media/azure-stack-tutorial-tenant-vm/image05.png)

1. <span data-ttu-id="daeb5-138">Select **Quotas**, and then select the first service that you want to create a quota for.</span><span class="sxs-lookup"><span data-stu-id="daeb5-138">Select **Quotas**, and then select the first service that you want to create a quota for.</span></span> <span data-ttu-id="daeb5-139">For an IaaS quota, use the following example as a guide for configuring quotas for the Compute, Network, and Storage services.</span><span class="sxs-lookup"><span data-stu-id="daeb5-139">For an IaaS quota, use the following example as a guide for configuring quotas for the Compute, Network, and Storage services.</span></span>

   - <span data-ttu-id="daeb5-140">First, create a quota for the Compute service.</span><span class="sxs-lookup"><span data-stu-id="daeb5-140">First, create a quota for the Compute service.</span></span> <span data-ttu-id="daeb5-141">In the namespace list, select **Microsoft.Compute** and then select **Create new quota**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-141">In the namespace list, select **Microsoft.Compute** and then select **Create new quota**.</span></span>

     ![Create new quota](media/azure-stack-tutorial-tenant-vm/image06.png)

   - <span data-ttu-id="daeb5-143">In **Create quota**, enter a name for the quota.</span><span class="sxs-lookup"><span data-stu-id="daeb5-143">In **Create quota**, enter a name for the quota.</span></span> <span data-ttu-id="daeb5-144">You can change or accept any of the quota values that are shown for the quota you're creating.</span><span class="sxs-lookup"><span data-stu-id="daeb5-144">You can change or accept any of the quota values that are shown for the quota you're creating.</span></span> <span data-ttu-id="daeb5-145">In this example, we accept the default settings and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-145">In this example, we accept the default settings and select **OK**.</span></span>

     ![Quota name](media/azure-stack-tutorial-tenant-vm/image07.png)

   - <span data-ttu-id="daeb5-147">Pick **Microsoft.Compute** in the namespace list, and then select the quota that you created.</span><span class="sxs-lookup"><span data-stu-id="daeb5-147">Pick **Microsoft.Compute** in the namespace list, and then select the quota that you created.</span></span> <span data-ttu-id="daeb5-148">This links the quota to the Compute service.</span><span class="sxs-lookup"><span data-stu-id="daeb5-148">This links the quota to the Compute service.</span></span>

     ![Select quota](media/azure-stack-tutorial-tenant-vm/image08.png)

      <span data-ttu-id="daeb5-150">Repeat these steps for the Network and Storage services.</span><span class="sxs-lookup"><span data-stu-id="daeb5-150">Repeat these steps for the Network and Storage services.</span></span> <span data-ttu-id="daeb5-151">When you're finished, select **OK** in **Quotas** to save all the quotas.</span><span class="sxs-lookup"><span data-stu-id="daeb5-151">When you're finished, select **OK** in **Quotas** to save all the quotas.</span></span>

1. <span data-ttu-id="daeb5-152">In **New plan**, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-152">In **New plan**, select **OK**.</span></span>

1. <span data-ttu-id="daeb5-153">Under **Plan**, select the new plan and then **Select**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-153">Under **Plan**, select the new plan and then **Select**.</span></span>

1. <span data-ttu-id="daeb5-154">In **New offer**, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-154">In **New offer**, select **Create**.</span></span> <span data-ttu-id="daeb5-155">You'll see a notification when the offer is created.</span><span class="sxs-lookup"><span data-stu-id="daeb5-155">You'll see a notification when the offer is created.</span></span>

1. <span data-ttu-id="daeb5-156">On the dashboard menu, select **Offers** and then pick the offer you created.</span><span class="sxs-lookup"><span data-stu-id="daeb5-156">On the dashboard menu, select **Offers** and then pick the offer you created.</span></span>

1. <span data-ttu-id="daeb5-157">Select **Change State**, and then chose **Public**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-157">Select **Change State**, and then chose **Public**.</span></span>

    ![Public state](media/azure-stack-tutorial-tenant-vm/image09.png)

## <a name="add-an-image"></a><span data-ttu-id="daeb5-159">Add an image</span><span class="sxs-lookup"><span data-stu-id="daeb5-159">Add an image</span></span>

<span data-ttu-id="daeb5-160">Before you can provision virtual machines, you must add an image to the Azure Stack marketplace.</span><span class="sxs-lookup"><span data-stu-id="daeb5-160">Before you can provision virtual machines, you must add an image to the Azure Stack marketplace.</span></span> <span data-ttu-id="daeb5-161">You can add the image of your choice, including Linux images, from the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="daeb5-161">You can add the image of your choice, including Linux images, from the Azure Marketplace.</span></span>

<span data-ttu-id="daeb5-162">If you are operating in a connected scenario and if you have registered your Azure Stack instance with Azure, then you can download the Windows Server 2016 VM image from the Azure Marketplace by using the steps described in the [Download marketplace items from Azure to Azure Stack](azure-stack-download-azure-marketplace-item.md) topic.</span><span class="sxs-lookup"><span data-stu-id="daeb5-162">If you are operating in a connected scenario and if you have registered your Azure Stack instance with Azure, then you can download the Windows Server 2016 VM image from the Azure Marketplace by using the steps described in the [Download marketplace items from Azure to Azure Stack](azure-stack-download-azure-marketplace-item.md) topic.</span></span>

<span data-ttu-id="daeb5-163">For information about adding different items to the marketplace, see [The Azure Stack Marketplace](azure-stack-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="daeb5-163">For information about adding different items to the marketplace, see [The Azure Stack Marketplace](azure-stack-marketplace.md).</span></span>

## <a name="test-the-offer"></a><span data-ttu-id="daeb5-164">Test the offer</span><span class="sxs-lookup"><span data-stu-id="daeb5-164">Test the offer</span></span>

<span data-ttu-id="daeb5-165">Now that you’ve created an offer, you can test it.</span><span class="sxs-lookup"><span data-stu-id="daeb5-165">Now that you’ve created an offer, you can test it.</span></span> <span data-ttu-id="daeb5-166">You'll sign in as a user, subscribe to the offer, and then add a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="daeb5-166">You'll sign in as a user, subscribe to the offer, and then add a virtual machine.</span></span>

1. <span data-ttu-id="daeb5-167">**Subscribe to an offer**</span><span class="sxs-lookup"><span data-stu-id="daeb5-167">**Subscribe to an offer**</span></span>

   <span data-ttu-id="daeb5-168">a.</span><span class="sxs-lookup"><span data-stu-id="daeb5-168">a.</span></span> <span data-ttu-id="daeb5-169">Sign in to the user portal with a user account and select the **Get a Subscription** tile.</span><span class="sxs-lookup"><span data-stu-id="daeb5-169">Sign in to the user portal with a user account and select the **Get a Subscription** tile.</span></span>
   - <span data-ttu-id="daeb5-170">For an integrated system, the URL varies based on your operator’s region and external domain name, and will be in the format https://portal.&lt;*region*&gt;.&lt;*FQDN*&gt;.</span><span class="sxs-lookup"><span data-stu-id="daeb5-170">For an integrated system, the URL varies based on your operator’s region and external domain name, and will be in the format https://portal.&lt;*region*&gt;.&lt;*FQDN*&gt;.</span></span>
   - <span data-ttu-id="daeb5-171">If you’re using the Azure Stack Development Kit, the portal address is https://portal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="daeb5-171">If you’re using the Azure Stack Development Kit, the portal address is https://portal.local.azurestack.external.</span></span>

   ![Get a subscription](media/azure-stack-subscribe-plan-provision-vm/image01.png)

   <span data-ttu-id="daeb5-173">b.</span><span class="sxs-lookup"><span data-stu-id="daeb5-173">b.</span></span> <span data-ttu-id="daeb5-174">In **Get a Subscription**, enter a name for your subscription in the **Display Name** field.</span><span class="sxs-lookup"><span data-stu-id="daeb5-174">In **Get a Subscription**, enter a name for your subscription in the **Display Name** field.</span></span> <span data-ttu-id="daeb5-175">Select **Offer**, and then choose one of the offers in the **Choose an offer** list.</span><span class="sxs-lookup"><span data-stu-id="daeb5-175">Select **Offer**, and then choose one of the offers in the **Choose an offer** list.</span></span> <span data-ttu-id="daeb5-176">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-176">Select **Create**.</span></span>

   ![Create an offer](media/azure-stack-subscribe-plan-provision-vm/image02.png)

   <span data-ttu-id="daeb5-178">c.</span><span class="sxs-lookup"><span data-stu-id="daeb5-178">c.</span></span> <span data-ttu-id="daeb5-179">To view the subscription, select **All services**, and then under the **GENERAL** category select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-179">To view the subscription, select **All services**, and then under the **GENERAL** category select **Subscriptions**.</span></span> <span data-ttu-id="daeb5-180">Select your new subscription to see which services are part of the subscription.</span><span class="sxs-lookup"><span data-stu-id="daeb5-180">Select your new subscription to see which services are part of the subscription.</span></span>

   >[!NOTE]
   ><span data-ttu-id="daeb5-181">After you subscribe to an offer, you might have to refresh the portal to see which services are part of the new subscription.</span><span class="sxs-lookup"><span data-stu-id="daeb5-181">After you subscribe to an offer, you might have to refresh the portal to see which services are part of the new subscription.</span></span>

1. <span data-ttu-id="daeb5-182">**Provision a virtual machine**</span><span class="sxs-lookup"><span data-stu-id="daeb5-182">**Provision a virtual machine**</span></span>

   <span data-ttu-id="daeb5-183">From the user portal you can provision a virtual machine using the new subscription.</span><span class="sxs-lookup"><span data-stu-id="daeb5-183">From the user portal you can provision a virtual machine using the new subscription.</span></span>

   <span data-ttu-id="daeb5-184">a.</span><span class="sxs-lookup"><span data-stu-id="daeb5-184">a.</span></span> <span data-ttu-id="daeb5-185">Sign in to the user portal with a user account.</span><span class="sxs-lookup"><span data-stu-id="daeb5-185">Sign in to the user portal with a user account.</span></span>
      - <span data-ttu-id="daeb5-186">For an integrated system, the URL varies based on your operator’s region and external domain name, and will be in the format https://portal.&lt;*region*&gt;.&lt;*FQDN*&gt;.</span><span class="sxs-lookup"><span data-stu-id="daeb5-186">For an integrated system, the URL varies based on your operator’s region and external domain name, and will be in the format https://portal.&lt;*region*&gt;.&lt;*FQDN*&gt;.</span></span>
   - <span data-ttu-id="daeb5-187">If you’re using the Azure Stack Development Kit, the portal address is https://portal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="daeb5-187">If you’re using the Azure Stack Development Kit, the portal address is https://portal.local.azurestack.external.</span></span>

   <span data-ttu-id="daeb5-188">b.</span><span class="sxs-lookup"><span data-stu-id="daeb5-188">b.</span></span>  <span data-ttu-id="daeb5-189">On the dashboard, select **New** > **Compute** > **Windows Server 2016 Datacenter Eval**, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-189">On the dashboard, select **New** > **Compute** > **Windows Server 2016 Datacenter Eval**, and then select **Create**.</span></span>

   <span data-ttu-id="daeb5-190">c.</span><span class="sxs-lookup"><span data-stu-id="daeb5-190">c.</span></span> <span data-ttu-id="daeb5-191">In **Basics**, provide the following information:</span><span class="sxs-lookup"><span data-stu-id="daeb5-191">In **Basics**, provide the following information:</span></span>
      - <span data-ttu-id="daeb5-192">Enter a **Name**</span><span class="sxs-lookup"><span data-stu-id="daeb5-192">Enter a **Name**</span></span>
      - <span data-ttu-id="daeb5-193">Enter a **User name**</span><span class="sxs-lookup"><span data-stu-id="daeb5-193">Enter a **User name**</span></span>
      - <span data-ttu-id="daeb5-194">Enter a **Password**</span><span class="sxs-lookup"><span data-stu-id="daeb5-194">Enter a **Password**</span></span>
      - <span data-ttu-id="daeb5-195">Choose a **Subscription**</span><span class="sxs-lookup"><span data-stu-id="daeb5-195">Choose a **Subscription**</span></span>
      - <span data-ttu-id="daeb5-196">Create a **Resource group** (or select an existing one.)</span><span class="sxs-lookup"><span data-stu-id="daeb5-196">Create a **Resource group** (or select an existing one.)</span></span> 
      - <span data-ttu-id="daeb5-197">Select **OK** to save this information.</span><span class="sxs-lookup"><span data-stu-id="daeb5-197">Select **OK** to save this information.</span></span>

   <span data-ttu-id="daeb5-198">d.</span><span class="sxs-lookup"><span data-stu-id="daeb5-198">d.</span></span> <span data-ttu-id="daeb5-199">In **Choose a size**, select **A1 Standard**, and then **Select**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-199">In **Choose a size**, select **A1 Standard**, and then **Select**.</span></span>  

   <span data-ttu-id="daeb5-200">e.</span><span class="sxs-lookup"><span data-stu-id="daeb5-200">e.</span></span> <span data-ttu-id="daeb5-201">In **Settings**, select **Virtual network**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-201">In **Settings**, select **Virtual network**.</span></span>

   <span data-ttu-id="daeb5-202">f.</span><span class="sxs-lookup"><span data-stu-id="daeb5-202">f.</span></span> <span data-ttu-id="daeb5-203">In **Choose virtual network**, select **Create new**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-203">In **Choose virtual network**, select **Create new**.</span></span>

   <span data-ttu-id="daeb5-204">g.</span><span class="sxs-lookup"><span data-stu-id="daeb5-204">g.</span></span> <span data-ttu-id="daeb5-205">In **Create virtual network**, accept all the defaults, and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-205">In **Create virtual network**, accept all the defaults, and select **OK**.</span></span>

   <span data-ttu-id="daeb5-206">h.</span><span class="sxs-lookup"><span data-stu-id="daeb5-206">h.</span></span> <span data-ttu-id="daeb5-207">Select **OK** in **Settings** to save the network configuration.</span><span class="sxs-lookup"><span data-stu-id="daeb5-207">Select **OK** in **Settings** to save the network configuration.</span></span>

   ![Create virtual network](media/azure-stack-provision-vm/image04.png)

   <span data-ttu-id="daeb5-209">i.</span><span class="sxs-lookup"><span data-stu-id="daeb5-209">i.</span></span> <span data-ttu-id="daeb5-210">In **Summary**, select **OK** to create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="daeb5-210">In **Summary**, select **OK** to create the virtual machine.</span></span>  

   <span data-ttu-id="daeb5-211">j.</span><span class="sxs-lookup"><span data-stu-id="daeb5-211">j.</span></span> <span data-ttu-id="daeb5-212">To see the new virtual machine, select **All resources**.</span><span class="sxs-lookup"><span data-stu-id="daeb5-212">To see the new virtual machine, select **All resources**.</span></span> <span data-ttu-id="daeb5-213">Search for the virtual machine and select its name from the search results.</span><span class="sxs-lookup"><span data-stu-id="daeb5-213">Search for the virtual machine and select its name from the search results.</span></span>

   ![All resources](media/azure-stack-provision-vm/image06.png)

## <a name="next-steps"></a><span data-ttu-id="daeb5-215">Next steps</span><span class="sxs-lookup"><span data-stu-id="daeb5-215">Next steps</span></span>

<span data-ttu-id="daeb5-216">In this tutorial you learned how to:</span><span class="sxs-lookup"><span data-stu-id="daeb5-216">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="daeb5-217">Create an offer</span><span class="sxs-lookup"><span data-stu-id="daeb5-217">Create an offer</span></span>
> * <span data-ttu-id="daeb5-218">Add an image</span><span class="sxs-lookup"><span data-stu-id="daeb5-218">Add an image</span></span>
> * <span data-ttu-id="daeb5-219">Test the offer</span><span class="sxs-lookup"><span data-stu-id="daeb5-219">Test the offer</span></span>

<span data-ttu-id="daeb5-220">Advance to the next tutorial to learn how to:</span><span class="sxs-lookup"><span data-stu-id="daeb5-220">Advance to the next tutorial to learn how to:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="daeb5-221">Make SQL databases available to your Azure Stack users</span><span class="sxs-lookup"><span data-stu-id="daeb5-221">Make SQL databases available to your Azure Stack users</span></span>](azure-stack-tutorial-sql-server.md)