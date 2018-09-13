---
title: Set up a lab account with Azure Lab Services | Microsoft Docs
description: In this tutorial, you set up a lab account with Azure Lab Services.
services: devtest-lab, lab-services, virtual-machines
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.custom: mvc
ms.date: 07/17/2018
ms.author: spelluru
ms.openlocfilehash: b60c1e84eb5b62bfce0eb2ba96129deeee2fc3c3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857041"
---
# <a name="tutorial-set-up-a-lab-account-with-azure-lab-services"></a><span data-ttu-id="87202-103">Tutorial: Set up a lab account with Azure Lab Services</span><span class="sxs-lookup"><span data-stu-id="87202-103">Tutorial: Set up a lab account with Azure Lab Services</span></span>
<span data-ttu-id="87202-104">In Azure Lab Services, a lab account serves as the central account in which your organization's labs are managed.</span><span class="sxs-lookup"><span data-stu-id="87202-104">In Azure Lab Services, a lab account serves as the central account in which your organization's labs are managed.</span></span> <span data-ttu-id="87202-105">In your lab account, give permission to others to create labs, and set policies that apply to all labs under the lab account.</span><span class="sxs-lookup"><span data-stu-id="87202-105">In your lab account, give permission to others to create labs, and set policies that apply to all labs under the lab account.</span></span> <span data-ttu-id="87202-106">In this tutorial, learn how to create a lab account as a lab administrator.</span><span class="sxs-lookup"><span data-stu-id="87202-106">In this tutorial, learn how to create a lab account as a lab administrator.</span></span> 

<span data-ttu-id="87202-107">In this tutorial, you do the following actions:</span><span class="sxs-lookup"><span data-stu-id="87202-107">In this tutorial, you do the following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="87202-108">Create a lab account</span><span class="sxs-lookup"><span data-stu-id="87202-108">Create a lab account</span></span>
> * <span data-ttu-id="87202-109">Add a user to the Lab Creator role</span><span class="sxs-lookup"><span data-stu-id="87202-109">Add a user to the Lab Creator role</span></span>
> * <span data-ttu-id="87202-110">Specify Marketplace images available for lab owners</span><span class="sxs-lookup"><span data-stu-id="87202-110">Specify Marketplace images available for lab owners</span></span>

<span data-ttu-id="87202-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="87202-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="create-a-lab-account"></a><span data-ttu-id="87202-112">Create a lab account</span><span class="sxs-lookup"><span data-stu-id="87202-112">Create a lab account</span></span>
<span data-ttu-id="87202-113">The following steps illustrate how to use the Azure portal to create a lab account with Azure Lab Services.</span><span class="sxs-lookup"><span data-stu-id="87202-113">The following steps illustrate how to use the Azure portal to create a lab account with Azure Lab Services.</span></span> 

1. <span data-ttu-id="87202-114">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="87202-114">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="87202-115">From the main menu on the left side, select **Create a resource**.</span><span class="sxs-lookup"><span data-stu-id="87202-115">From the main menu on the left side, select **Create a resource**.</span></span>
3. <span data-ttu-id="87202-116">Search for **Lab Services** in the Azure Marketplace, and select **Lab Services** in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="87202-116">Search for **Lab Services** in the Azure Marketplace, and select **Lab Services** in the drop-down list.</span></span> 
4. <span data-ttu-id="87202-117">Select **Lab Services (Preview)** in the filtered list of services.</span><span class="sxs-lookup"><span data-stu-id="87202-117">Select **Lab Services (Preview)** in the filtered list of services.</span></span> 
1. <span data-ttu-id="87202-118">In the **Create a lab account** window, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="87202-118">In the **Create a lab account** window, select **Create**.</span></span>
2. <span data-ttu-id="87202-119">In the **Lab account** window, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="87202-119">In the **Lab account** window, do the following actions:</span></span> 
    1. <span data-ttu-id="87202-120">For **Lab account name**, enter a name.</span><span class="sxs-lookup"><span data-stu-id="87202-120">For **Lab account name**, enter a name.</span></span> 
    2. <span data-ttu-id="87202-121">Select the **Azure subscription** in which you want to create the lab account.</span><span class="sxs-lookup"><span data-stu-id="87202-121">Select the **Azure subscription** in which you want to create the lab account.</span></span>
    3. <span data-ttu-id="87202-122">For **Resource group**, select **Create new**, and enter a name for the resource group.</span><span class="sxs-lookup"><span data-stu-id="87202-122">For **Resource group**, select **Create new**, and enter a name for the resource group.</span></span>
    4. <span data-ttu-id="87202-123">For **Location**, select a location/region in which you want the lab account to be created.</span><span class="sxs-lookup"><span data-stu-id="87202-123">For **Location**, select a location/region in which you want the lab account to be created.</span></span> 
    5. <span data-ttu-id="87202-124">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="87202-124">Select **Create**.</span></span> 

        ![Create a lab account window](../media/tutorial-setup-lab-account/lab-account-settings.png)
5. <span data-ttu-id="87202-126">If you don't see the page for the lab account, select the **notifications** button, and then click **Go to resource** button in the notifications.</span><span class="sxs-lookup"><span data-stu-id="87202-126">If you don't see the page for the lab account, select the **notifications** button, and then click **Go to resource** button in the notifications.</span></span> 

    ![Create a lab account window](../media/tutorial-setup-lab-account/notification-go-to-resource.png)    
6. <span data-ttu-id="87202-128">You see the following **lab account** page:</span><span class="sxs-lookup"><span data-stu-id="87202-128">You see the following **lab account** page:</span></span>

    ![Lab account page](../media/tutorial-setup-lab-account/lab-account-page.png)

## <a name="add-a-user-to-the-lab-creator-role"></a><span data-ttu-id="87202-130">Add a user to the Lab Creator role</span><span class="sxs-lookup"><span data-stu-id="87202-130">Add a user to the Lab Creator role</span></span>
<span data-ttu-id="87202-131">To set up a classroom lab in a lab account, the user must be a member of the **Lab Creator** role in the lab account.</span><span class="sxs-lookup"><span data-stu-id="87202-131">To set up a classroom lab in a lab account, the user must be a member of the **Lab Creator** role in the lab account.</span></span> <span data-ttu-id="87202-132">The account you used to create the lab account is automatically added to this role.</span><span class="sxs-lookup"><span data-stu-id="87202-132">The account you used to create the lab account is automatically added to this role.</span></span> <span data-ttu-id="87202-133">If you are planning to use the same user account to create a classroom lab, you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="87202-133">If you are planning to use the same user account to create a classroom lab, you can skip this step.</span></span> <span data-ttu-id="87202-134">To use another user account to create a classroom lab, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="87202-134">To use another user account to create a classroom lab, do the following steps:</span></span> 

<span data-ttu-id="87202-135">To provide educators the permission to create labs for their classes, add them to the **Lab Creator** role:</span><span class="sxs-lookup"><span data-stu-id="87202-135">To provide educators the permission to create labs for their classes, add them to the **Lab Creator** role:</span></span>

1. <span data-ttu-id="87202-136">On the **Lab Account** page, select **Access control (IAM)**, and click **+ Add** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="87202-136">On the **Lab Account** page, select **Access control (IAM)**, and click **+ Add** on the toolbar.</span></span> 

    ![Lab account page](../media/tutorial-setup-lab-account/access-control.png)
2. <span data-ttu-id="87202-138">On the **Add permissions** page, select **Lab Creator** for **Role**, select the user you want to add to the Lab Creators role, and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="87202-138">On the **Add permissions** page, select **Lab Creator** for **Role**, select the user you want to add to the Lab Creators role, and select **Save**.</span></span> 

    ![Add user to the Lab Creator role](../media/tutorial-setup-lab-account/add-user-to-lab-creator-role.png)

## <a name="specify-marketplace-images-available-to-lab-owners"></a><span data-ttu-id="87202-140">Specify Marketplace images available to lab owners</span><span class="sxs-lookup"><span data-stu-id="87202-140">Specify Marketplace images available to lab owners</span></span>
<span data-ttu-id="87202-141">As a lab account owner, you can specify the Marketplace images that lab creators can use to create labs in the lab account.</span><span class="sxs-lookup"><span data-stu-id="87202-141">As a lab account owner, you can specify the Marketplace images that lab creators can use to create labs in the lab account.</span></span> 

1. <span data-ttu-id="87202-142">Select **Marketplace images** on the menu to the left.</span><span class="sxs-lookup"><span data-stu-id="87202-142">Select **Marketplace images** on the menu to the left.</span></span> <span data-ttu-id="87202-143">By default, you see the full list of images (both enabled and disabled).</span><span class="sxs-lookup"><span data-stu-id="87202-143">By default, you see the full list of images (both enabled and disabled).</span></span> <span data-ttu-id="87202-144">You can filter the list to see only enabled/disabled images by selecting the **Enabled only**/**Disabled only** option from the drop-down list at the top.</span><span class="sxs-lookup"><span data-stu-id="87202-144">You can filter the list to see only enabled/disabled images by selecting the **Enabled only**/**Disabled only** option from the drop-down list at the top.</span></span> 
    
    ![Marketplace images page](../media/tutorial-setup-lab-account/marketplace-images-page.png)

    <span data-ttu-id="87202-146">The Marketplace images that are displayed in the list are only the ones that satisfy the following conditions:</span><span class="sxs-lookup"><span data-stu-id="87202-146">The Marketplace images that are displayed in the list are only the ones that satisfy the following conditions:</span></span>
        
    - <span data-ttu-id="87202-147">Creates a single VM.</span><span class="sxs-lookup"><span data-stu-id="87202-147">Creates a single VM.</span></span>
    - <span data-ttu-id="87202-148">Uses Azure Resource Manager to provision VMs</span><span class="sxs-lookup"><span data-stu-id="87202-148">Uses Azure Resource Manager to provision VMs</span></span>
    - <span data-ttu-id="87202-149">Doesn't require purchasing an extra licensing plan</span><span class="sxs-lookup"><span data-stu-id="87202-149">Doesn't require purchasing an extra licensing plan</span></span>
2. <span data-ttu-id="87202-150">To **disable** a Marketplace image that has been enabled, do one of the following actions:</span><span class="sxs-lookup"><span data-stu-id="87202-150">To **disable** a Marketplace image that has been enabled, do one of the following actions:</span></span> 
    1. <span data-ttu-id="87202-151">Select **... (ellipsis)** in the last column, and select **Disable image**.</span><span class="sxs-lookup"><span data-stu-id="87202-151">Select **... (ellipsis)** in the last column, and select **Disable image**.</span></span> 

        ![Disable one image](../media/tutorial-setup-lab-account/disable-one-image.png) 
    2. <span data-ttu-id="87202-153">Select one or more images from the list by selecting the checkboxes before the image names in the list, and select **Disable selected images**.</span><span class="sxs-lookup"><span data-stu-id="87202-153">Select one or more images from the list by selecting the checkboxes before the image names in the list, and select **Disable selected images**.</span></span> 

        ![Disable multiple images](../media/tutorial-setup-lab-account/disable-multiple-images.png) 
1. <span data-ttu-id="87202-155">Similarly, to **enable** a Marketplace image, do one of the following actions:</span><span class="sxs-lookup"><span data-stu-id="87202-155">Similarly, to **enable** a Marketplace image, do one of the following actions:</span></span> 
    1. <span data-ttu-id="87202-156">Select **... (ellipsis)** in the last column, and select **Enable image**.</span><span class="sxs-lookup"><span data-stu-id="87202-156">Select **... (ellipsis)** in the last column, and select **Enable image**.</span></span> 
    2. <span data-ttu-id="87202-157">Select one or more images from the list by selecting the checkboxes before the image names in the list, and select **Enable selected images**.</span><span class="sxs-lookup"><span data-stu-id="87202-157">Select one or more images from the list by selecting the checkboxes before the image names in the list, and select **Enable selected images**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="87202-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="87202-158">Next steps</span></span>
<span data-ttu-id="87202-159">In this tutorial, you created a lab account.</span><span class="sxs-lookup"><span data-stu-id="87202-159">In this tutorial, you created a lab account.</span></span> <span data-ttu-id="87202-160">To learn about how to create a classroom lab as a profession, advance to the next tutorial:</span><span class="sxs-lookup"><span data-stu-id="87202-160">To learn about how to create a classroom lab as a profession, advance to the next tutorial:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="87202-161">Set up a classroom lab</span><span class="sxs-lookup"><span data-stu-id="87202-161">Set up a classroom lab</span></span>](tutorial-setup-classroom-lab.md)

