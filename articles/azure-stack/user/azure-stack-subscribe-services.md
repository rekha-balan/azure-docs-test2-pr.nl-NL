---
title: In this tutorial, you learn how to subscribe to an Azure Stack offer | Microsoft Docs
description: This tutorial shows you how to create a new subscription to Azure Stack services and test the offer by creating a test virtual machine.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.custom: mvc
ms.date: 09/05/2018
ms.author: brenduns
ms.reviewer: ''
ms.openlocfilehash: 0e2fa9b01d27d68c1eab9097a20b6e350ba47f99
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865778"
---
# <a name="tutorial-create-and-test-a-subscription"></a><span data-ttu-id="c3487-103">Tutorial: create and test a subscription</span><span class="sxs-lookup"><span data-stu-id="c3487-103">Tutorial: create and test a subscription</span></span>
<span data-ttu-id="c3487-104">This tutorial shows you how to create a subscription containing an offer and then test it.</span><span class="sxs-lookup"><span data-stu-id="c3487-104">This tutorial shows you how to create a subscription containing an offer and then test it.</span></span> <span data-ttu-id="c3487-105">For the test, you will sign in to the Azure Stack user portal as a cloud administrator, subscribe to the offer, and then create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c3487-105">For the test, you will sign in to the Azure Stack user portal as a cloud administrator, subscribe to the offer, and then create a virtual machine.</span></span>

> [!TIP]
> <span data-ttu-id="c3487-106">For more a more advanced evaluation experience, you can [create a subscription for a particular user](https://docs.microsoft.com/azure/azure-stack/azure-stack-subscribe-plan-provision-vm#create-a-subscription-as-a-cloud-operator) and then login as that user in the user portal.</span><span class="sxs-lookup"><span data-stu-id="c3487-106">For more a more advanced evaluation experience, you can [create a subscription for a particular user](https://docs.microsoft.com/azure/azure-stack/azure-stack-subscribe-plan-provision-vm#create-a-subscription-as-a-cloud-operator) and then login as that user in the user portal.</span></span> 

<span data-ttu-id="c3487-107">This tutorial shows you how to subscribe to an Azure Stack offer.</span><span class="sxs-lookup"><span data-stu-id="c3487-107">This tutorial shows you how to subscribe to an Azure Stack offer.</span></span>

<span data-ttu-id="c3487-108">What you will learn:</span><span class="sxs-lookup"><span data-stu-id="c3487-108">What you will learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c3487-109">Subscribe to an offer</span><span class="sxs-lookup"><span data-stu-id="c3487-109">Subscribe to an offer</span></span> 
> * <span data-ttu-id="c3487-110">Test the offer</span><span class="sxs-lookup"><span data-stu-id="c3487-110">Test the offer</span></span>

## <a name="subscribe-to-an-offer"></a><span data-ttu-id="c3487-111">Subscribe to an offer</span><span class="sxs-lookup"><span data-stu-id="c3487-111">Subscribe to an offer</span></span>
<span data-ttu-id="c3487-112">To subscribe to an offer as a user, you need to login to the Azure Stack user portal to discover the services that have been offered by the Azure Stack operator.</span><span class="sxs-lookup"><span data-stu-id="c3487-112">To subscribe to an offer as a user, you need to login to the Azure Stack user portal to discover the services that have been offered by the Azure Stack operator.</span></span>

1. <span data-ttu-id="c3487-113">Sign in to the user portal and click **Get a Subscription**.</span><span class="sxs-lookup"><span data-stu-id="c3487-113">Sign in to the user portal and click **Get a Subscription**.</span></span>

   ![Get a subscription](media/azure-stack-subscribe-services/get-subscription.png)

2. <span data-ttu-id="c3487-115">In the **Display Name** field, type a name for your subscription.</span><span class="sxs-lookup"><span data-stu-id="c3487-115">In the **Display Name** field, type a name for your subscription.</span></span> <span data-ttu-id="c3487-116">Then, click **Offer** to select one of the available offers in the **Choose an offer** section and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c3487-116">Then, click **Offer** to select one of the available offers in the **Choose an offer** section and then click **Create**.</span></span>

   ![Create an offer](media/azure-stack-subscribe-services/create-subscription.png)

   > [!TIP]
   > <span data-ttu-id="c3487-118">You must now refresh the user portal to start using your subscription.</span><span class="sxs-lookup"><span data-stu-id="c3487-118">You must now refresh the user portal to start using your subscription.</span></span>

3. <span data-ttu-id="c3487-119">To view the subscription you created, click **All services**.</span><span class="sxs-lookup"><span data-stu-id="c3487-119">To view the subscription you created, click **All services**.</span></span>  <span data-ttu-id="c3487-120">Then, under the **GENERAL** category select **Subscriptions**, and then select your new subscription.</span><span class="sxs-lookup"><span data-stu-id="c3487-120">Then, under the **GENERAL** category select **Subscriptions**, and then select your new subscription.</span></span> <span data-ttu-id="c3487-121">After you subscribe to an offer, refresh the portal to see if new services have been included as part of the new subscription.</span><span class="sxs-lookup"><span data-stu-id="c3487-121">After you subscribe to an offer, refresh the portal to see if new services have been included as part of the new subscription.</span></span> <span data-ttu-id="c3487-122">In this example, **Virtual machines** has been added.</span><span class="sxs-lookup"><span data-stu-id="c3487-122">In this example, **Virtual machines** has been added.</span></span>

   ![View subscription](media/azure-stack-subscribe-services/view-subscription.png)


## <a name="test-the-offer"></a><span data-ttu-id="c3487-124">Test the offer</span><span class="sxs-lookup"><span data-stu-id="c3487-124">Test the offer</span></span>
<span data-ttu-id="c3487-125">While logged in to the user portal, you can test the offer by provisioning a virtual machine using the new subscription capabilities.</span><span class="sxs-lookup"><span data-stu-id="c3487-125">While logged in to the user portal, you can test the offer by provisioning a virtual machine using the new subscription capabilities.</span></span> 

> [!NOTE]
> <span data-ttu-id="c3487-126">This test requires that a Windows Server 2016 Datacenter VM has first been added to the Azure Stack marketplace.</span><span class="sxs-lookup"><span data-stu-id="c3487-126">This test requires that a Windows Server 2016 Datacenter VM has first been added to the Azure Stack marketplace.</span></span> 

1. <span data-ttu-id="c3487-127">Sign in to the user portal.</span><span class="sxs-lookup"><span data-stu-id="c3487-127">Sign in to the user portal.</span></span>

2. <span data-ttu-id="c3487-128">In the user portal, click **Virtual Machines** > **Add** > **Windows Server 2016 Datacenter**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c3487-128">In the user portal, click **Virtual Machines** > **Add** > **Windows Server 2016 Datacenter**, and then click **Create**.</span></span>

3. <span data-ttu-id="c3487-129">In the **Basics** section, type a **Name**, **User name**, and **Password**, choose a **Subscription**, create a **Resource group** (or select an existing one), and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c3487-129">In the **Basics** section, type a **Name**, **User name**, and **Password**, choose a **Subscription**, create a **Resource group** (or select an existing one), and then click **OK**.</span></span>

4. <span data-ttu-id="c3487-130">In the **Choose a size** section, click **A1 Standard**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="c3487-130">In the **Choose a size** section, click **A1 Standard**, and then click **Select**.</span></span>  

5. <span data-ttu-id="c3487-131">In the Settings blade, accept the defaults and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c3487-131">In the Settings blade, accept the defaults and click **OK**.</span></span>

6. <span data-ttu-id="c3487-132">In the **Summary** section, click **OK** to create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="c3487-132">In the **Summary** section, click **OK** to create the virtual machine.</span></span>  

7. <span data-ttu-id="c3487-133">To see your new virtual machine, click **Virtual machines**, then search for the new virtual machine, and click its name.</span><span class="sxs-lookup"><span data-stu-id="c3487-133">To see your new virtual machine, click **Virtual machines**, then search for the new virtual machine, and click its name.</span></span>

    ![All resources](media/azure-stack-subscribe-services/view-vm.png)

> [!NOTE]
> <span data-ttu-id="c3487-135">The virtual machine deployment will take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="c3487-135">The virtual machine deployment will take a few minutes to complete.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c3487-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="c3487-136">Next steps</span></span>

<span data-ttu-id="c3487-137">What you learned in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="c3487-137">What you learned in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c3487-138">Subscribe to an offer</span><span class="sxs-lookup"><span data-stu-id="c3487-138">Subscribe to an offer</span></span> 
> * <span data-ttu-id="c3487-139">Test the offer</span><span class="sxs-lookup"><span data-stu-id="c3487-139">Test the offer</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="c3487-140">Create a VM from a community template</span><span class="sxs-lookup"><span data-stu-id="c3487-140">Create a VM from a community template</span></span>](azure-stack-create-vm-template.md)