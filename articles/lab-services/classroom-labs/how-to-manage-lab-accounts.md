---
title: Manage lab accounts in Azure Lab Services | Microsoft Docs
description: Learn how to create a lab account, view all lab accounts, or delete a lab account in an Azure subscription.
services: lab-services
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2018
ms.author: spelluru
ms.openlocfilehash: fd43c62f1a291a59d5d373437a49b263d6af4cb3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868781"
---
# <a name="manage-lab-accounts-in-azure-lab-services"></a><span data-ttu-id="bfb1c-103">Manage lab accounts in Azure Lab Services</span><span class="sxs-lookup"><span data-stu-id="bfb1c-103">Manage lab accounts in Azure Lab Services</span></span> 
<span data-ttu-id="bfb1c-104">In Azure Lab Services, a lab account is a container for managed labs such as classroom labs.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-104">In Azure Lab Services, a lab account is a container for managed labs such as classroom labs.</span></span> <span data-ttu-id="bfb1c-105">An administrator sets up a lab account with Azure Lab Services and provides access to lab owners who can create labs in the account.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-105">An administrator sets up a lab account with Azure Lab Services and provides access to lab owners who can create labs in the account.</span></span> <span data-ttu-id="bfb1c-106">This article describes how to create a lab account, view all lab accounts, or delete a lab account.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-106">This article describes how to create a lab account, view all lab accounts, or delete a lab account.</span></span>

## <a name="create-a-lab-account"></a><span data-ttu-id="bfb1c-107">Create a lab account</span><span class="sxs-lookup"><span data-stu-id="bfb1c-107">Create a lab account</span></span>
1. <span data-ttu-id="bfb1c-108">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bfb1c-108">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bfb1c-109">From the main menu on the left side, select **Create a resource**.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-109">From the main menu on the left side, select **Create a resource**.</span></span>
3. <span data-ttu-id="bfb1c-110">Search for **Lab Services** in the Azure Marketplace, and select **Lab Services** in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-110">Search for **Lab Services** in the Azure Marketplace, and select **Lab Services** in the drop-down list.</span></span> 
4. <span data-ttu-id="bfb1c-111">Select **Lab Services (Preview)** in the filtered list of services.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-111">Select **Lab Services (Preview)** in the filtered list of services.</span></span> 
5. <span data-ttu-id="bfb1c-112">In the **Create a lab account** window, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-112">In the **Create a lab account** window, select **Create**.</span></span>
7. <span data-ttu-id="bfb1c-113">In the **Lab account** window, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="bfb1c-113">In the **Lab account** window, do the following actions:</span></span> 
    1. <span data-ttu-id="bfb1c-114">For **Lab account name**, enter a name.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-114">For **Lab account name**, enter a name.</span></span> 
    2. <span data-ttu-id="bfb1c-115">Select the **Azure subscription** in which you want to create the lab account.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-115">Select the **Azure subscription** in which you want to create the lab account.</span></span>
    3. <span data-ttu-id="bfb1c-116">For **Resource group**, select **Create new**, and enter a name for the resource group.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-116">For **Resource group**, select **Create new**, and enter a name for the resource group.</span></span>
    4. <span data-ttu-id="bfb1c-117">For **Location**, select a location/region in which you want the lab account to be created.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-117">For **Location**, select a location/region in which you want the lab account to be created.</span></span> 
    5. <span data-ttu-id="bfb1c-118">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-118">Select **Create**.</span></span> 

        ![Create a lab account window](../media/how-to-manage-lab-accounts/lab-account-settings.png)
5. <span data-ttu-id="bfb1c-120">If you don't see the page for the lab account, select the **notifications** button, and then click **Go to resource** button in the notifications.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-120">If you don't see the page for the lab account, select the **notifications** button, and then click **Go to resource** button in the notifications.</span></span> 

    ![Create a lab account window](../media/how-to-manage-lab-accounts/notification-go-to-resource.png)    
6. <span data-ttu-id="bfb1c-122">You see the following **lab account** page:</span><span class="sxs-lookup"><span data-stu-id="bfb1c-122">You see the following **lab account** page:</span></span>

    ![Lab account page](../media/how-to-manage-lab-accounts/lab-account-page.png)

## <a name="add-a-user-to-the-lab-creator-role"></a><span data-ttu-id="bfb1c-124">Add a user to the Lab Creator role</span><span class="sxs-lookup"><span data-stu-id="bfb1c-124">Add a user to the Lab Creator role</span></span>
<span data-ttu-id="bfb1c-125">To set up a classroom lab in a lab account, the user must be a member of the **Lab Creator** role in the lab account.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-125">To set up a classroom lab in a lab account, the user must be a member of the **Lab Creator** role in the lab account.</span></span> <span data-ttu-id="bfb1c-126">The account you used to create the lab account is automatically added to this role.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-126">The account you used to create the lab account is automatically added to this role.</span></span> <span data-ttu-id="bfb1c-127">If you are planning to use the same user account to create a classroom lab, you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-127">If you are planning to use the same user account to create a classroom lab, you can skip this step.</span></span> <span data-ttu-id="bfb1c-128">To use another user account to create a classroom lab, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="bfb1c-128">To use another user account to create a classroom lab, do the following steps:</span></span> 

1. <span data-ttu-id="bfb1c-129">On the **Lab Account** page, select **Access control (IAM)**, and click **+ Add** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-129">On the **Lab Account** page, select **Access control (IAM)**, and click **+ Add** on the toolbar.</span></span> 

    ![Lab account page](../media/tutorial-setup-lab-account/access-control.png)
2. <span data-ttu-id="bfb1c-131">On the **Add permissions** page, select **Lab Creator** for **Role**, select the user you want to add to the Lab Creators role, and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-131">On the **Add permissions** page, select **Lab Creator** for **Role**, select the user you want to add to the Lab Creators role, and select **Save**.</span></span> 

    ![Add user to the Lab Creator role](../media/tutorial-setup-lab-account/add-user-to-lab-creator-role.png)

## <a name="specify-marketplace-images-available-to-lab-owners"></a><span data-ttu-id="bfb1c-133">Specify Marketplace images available to lab owners</span><span class="sxs-lookup"><span data-stu-id="bfb1c-133">Specify Marketplace images available to lab owners</span></span>
<span data-ttu-id="bfb1c-134">As a lab account owner, you can specify the Marketplace images that lab creators can use to create labs in the lab account.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-134">As a lab account owner, you can specify the Marketplace images that lab creators can use to create labs in the lab account.</span></span> 

1. <span data-ttu-id="bfb1c-135">Select **Marketplace images** on the menu to the left.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-135">Select **Marketplace images** on the menu to the left.</span></span> <span data-ttu-id="bfb1c-136">By default, you see the full list of images (both enabled and disabled).</span><span class="sxs-lookup"><span data-stu-id="bfb1c-136">By default, you see the full list of images (both enabled and disabled).</span></span> <span data-ttu-id="bfb1c-137">You can filter the list to see only enabled/disabled images by selecting the **Enabled only**/**Disabled only** option from the drop-down list at the top.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-137">You can filter the list to see only enabled/disabled images by selecting the **Enabled only**/**Disabled only** option from the drop-down list at the top.</span></span> 
    
    ![Marketplace images page](../media/tutorial-setup-lab-account/marketplace-images-page.png)

    <span data-ttu-id="bfb1c-139">The Marketplace images that are displayed in the list are only the ones that satisfy the following conditions:</span><span class="sxs-lookup"><span data-stu-id="bfb1c-139">The Marketplace images that are displayed in the list are only the ones that satisfy the following conditions:</span></span>
        
    - <span data-ttu-id="bfb1c-140">Creates a single VM.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-140">Creates a single VM.</span></span>
    - <span data-ttu-id="bfb1c-141">Uses Azure Resource Manager to provision VMs</span><span class="sxs-lookup"><span data-stu-id="bfb1c-141">Uses Azure Resource Manager to provision VMs</span></span>
    - <span data-ttu-id="bfb1c-142">Doesn't require purchasing an extra licensing plan</span><span class="sxs-lookup"><span data-stu-id="bfb1c-142">Doesn't require purchasing an extra licensing plan</span></span>
2. <span data-ttu-id="bfb1c-143">To **disable** a Marketplace image that has been enabled, do one of the following actions:</span><span class="sxs-lookup"><span data-stu-id="bfb1c-143">To **disable** a Marketplace image that has been enabled, do one of the following actions:</span></span> 
    1. <span data-ttu-id="bfb1c-144">Select **... (ellipsis)** in the last column, and select **Disable image**.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-144">Select **... (ellipsis)** in the last column, and select **Disable image**.</span></span> 

        ![Disable one image](../media/tutorial-setup-lab-account/disable-one-image.png) 
    2. <span data-ttu-id="bfb1c-146">Select one or more images from the list by selecting the checkboxes before the image names in the list, and select **Disable selected images**.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-146">Select one or more images from the list by selecting the checkboxes before the image names in the list, and select **Disable selected images**.</span></span> 

        ![Disable multiple images](../media/tutorial-setup-lab-account/disable-multiple-images.png) 
1. <span data-ttu-id="bfb1c-148">Similarly, to **enable** a Marketplace image, do one of the following actions:</span><span class="sxs-lookup"><span data-stu-id="bfb1c-148">Similarly, to **enable** a Marketplace image, do one of the following actions:</span></span> 
    1. <span data-ttu-id="bfb1c-149">Select **... (ellipsis)** in the last column, and select **Enable image**.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-149">Select **... (ellipsis)** in the last column, and select **Enable image**.</span></span> 
    2. <span data-ttu-id="bfb1c-150">Select one or more images from the list by selecting the checkboxes before the image names in the list, and select **Enable selected images**.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-150">Select one or more images from the list by selecting the checkboxes before the image names in the list, and select **Enable selected images**.</span></span> 

## <a name="view-lab-accounts"></a><span data-ttu-id="bfb1c-151">View lab accounts</span><span class="sxs-lookup"><span data-stu-id="bfb1c-151">View lab accounts</span></span>
1. <span data-ttu-id="bfb1c-152">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bfb1c-152">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bfb1c-153">Select **All resources** from the menu.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-153">Select **All resources** from the menu.</span></span> 
3. <span data-ttu-id="bfb1c-154">Select **Lab Services** for the **type**.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-154">Select **Lab Services** for the **type**.</span></span> 
    <span data-ttu-id="bfb1c-155">You can also filter by subscription, resource group, locations, and tags.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-155">You can also filter by subscription, resource group, locations, and tags.</span></span> 

## <a name="delete-a-lab-account"></a><span data-ttu-id="bfb1c-156">Delete a lab account</span><span class="sxs-lookup"><span data-stu-id="bfb1c-156">Delete a lab account</span></span>
<span data-ttu-id="bfb1c-157">Follow instructions from the previous section that displays lab accounts in a list.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-157">Follow instructions from the previous section that displays lab accounts in a list.</span></span> <span data-ttu-id="bfb1c-158">Use the following instructions to delete a lab account:</span><span class="sxs-lookup"><span data-stu-id="bfb1c-158">Use the following instructions to delete a lab account:</span></span> 

1. <span data-ttu-id="bfb1c-159">Select the **lab account** that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-159">Select the **lab account** that you want to delete.</span></span> 
2. <span data-ttu-id="bfb1c-160">Select **Delete** from the toolbar.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-160">Select **Delete** from the toolbar.</span></span> 
3. <span data-ttu-id="bfb1c-161">Type **Yes** for confirmation.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-161">Type **Yes** for confirmation.</span></span>
4. <span data-ttu-id="bfb1c-162">Select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="bfb1c-162">Select **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bfb1c-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="bfb1c-163">Next steps</span></span>
<span data-ttu-id="bfb1c-164">Get started with setting up a lab using Azure Lab Services:</span><span class="sxs-lookup"><span data-stu-id="bfb1c-164">Get started with setting up a lab using Azure Lab Services:</span></span>

- [<span data-ttu-id="bfb1c-165">Set up a classroom lab</span><span class="sxs-lookup"><span data-stu-id="bfb1c-165">Set up a classroom lab</span></span>](tutorial-setup-classroom-lab.md)
- [<span data-ttu-id="bfb1c-166">Set up a lab</span><span class="sxs-lookup"><span data-stu-id="bfb1c-166">Set up a lab</span></span>](../tutorial-create-custom-lab.md)
