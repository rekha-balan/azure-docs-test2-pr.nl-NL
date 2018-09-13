---
title: Manage Azure Stack storage accounts  | Microsoft Docs
description: Learn how to find, manage, recover and reclaim Azure Stack storage accounts
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.assetid: 627d355b-4812-45cb-bc1e-ce62476dab34
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: get-started-article
ms.date: 05/10/2018
ms.author: mabrigg
ms.reviewer: xiaofmao
ms.openlocfilehash: 8914391a586bb508192200beaba7f591649a1e99
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44815989"
---
# <a name="manage-storage-accounts-in-azure-stack"></a><span data-ttu-id="b1030-103">Manage storage accounts in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b1030-103">Manage storage accounts in Azure Stack</span></span>
<span data-ttu-id="b1030-104">Learn how to manage storage accounts in Azure Stack to find, recover, and reclaim storage capacity based on business needs.</span><span class="sxs-lookup"><span data-stu-id="b1030-104">Learn how to manage storage accounts in Azure Stack to find, recover, and reclaim storage capacity based on business needs.</span></span>

## <a name="find"></a><span data-ttu-id="b1030-105">Find a storage account</span><span class="sxs-lookup"><span data-stu-id="b1030-105">Find a storage account</span></span>
<span data-ttu-id="b1030-106">The list of storage accounts in the region can be viewed in Azure Stack by:</span><span class="sxs-lookup"><span data-stu-id="b1030-106">The list of storage accounts in the region can be viewed in Azure Stack by:</span></span>

1. <span data-ttu-id="b1030-107">In an Internet browser, navigate to https://adminportal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="b1030-107">In an Internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="b1030-108">Sign in to the Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span><span class="sxs-lookup"><span data-stu-id="b1030-108">Sign in to the Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="b1030-109">On the default dashboard – find the **Region management** list and select the region you want to explore, for example **(local**).</span><span class="sxs-lookup"><span data-stu-id="b1030-109">On the default dashboard – find the **Region management** list and select the region you want to explore, for example **(local**).</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image1.png)
4. <span data-ttu-id="b1030-110">Select **Storage** from the **Resource Providers** list.</span><span class="sxs-lookup"><span data-stu-id="b1030-110">Select **Storage** from the **Resource Providers** list.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image2.png)
5. <span data-ttu-id="b1030-111">Now, on the storage Resource Provider administrator pane – scroll down to the **Storage accounts** tab and select it.</span><span class="sxs-lookup"><span data-stu-id="b1030-111">Now, on the storage Resource Provider administrator pane – scroll down to the **Storage accounts** tab and select it.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image3.png)
   
   <span data-ttu-id="b1030-112">The resulting page is the list of storage accounts in that region.</span><span class="sxs-lookup"><span data-stu-id="b1030-112">The resulting page is the list of storage accounts in that region.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image4.png)

<span data-ttu-id="b1030-113">By default, the first 10 accounts are displayed.</span><span class="sxs-lookup"><span data-stu-id="b1030-113">By default, the first 10 accounts are displayed.</span></span> <span data-ttu-id="b1030-114">You can choose to fetch more by clicking the  **Load more** link at the bottom of the list.</span><span class="sxs-lookup"><span data-stu-id="b1030-114">You can choose to fetch more by clicking the  **Load more** link at the bottom of the list.</span></span>

<span data-ttu-id="b1030-115">OR</span><span class="sxs-lookup"><span data-stu-id="b1030-115">OR</span></span>

<span data-ttu-id="b1030-116">If you are interested in a particular storage account – you can **filter and fetch the relevant accounts** only.</span><span class="sxs-lookup"><span data-stu-id="b1030-116">If you are interested in a particular storage account – you can **filter and fetch the relevant accounts** only.</span></span>


<span data-ttu-id="b1030-117">**To filter for accounts:**</span><span class="sxs-lookup"><span data-stu-id="b1030-117">**To filter for accounts:**</span></span>

1. <span data-ttu-id="b1030-118">Select **Filter** at the top of the pane.</span><span class="sxs-lookup"><span data-stu-id="b1030-118">Select **Filter** at the top of the pane.</span></span>
2. <span data-ttu-id="b1030-119">On the Filter pane, it allows you to specify **account name**, \*\*subscription ID, or **status** to fine-tune the list of storage accounts to be displayed.</span><span class="sxs-lookup"><span data-stu-id="b1030-119">On the Filter pane, it allows you to specify **account name**, \*\*subscription ID, or **status** to fine-tune the list of storage accounts to be displayed.</span></span> <span data-ttu-id="b1030-120">Use them as appropriate.</span><span class="sxs-lookup"><span data-stu-id="b1030-120">Use them as appropriate.</span></span>
3. <span data-ttu-id="b1030-121">Select **Update**.</span><span class="sxs-lookup"><span data-stu-id="b1030-121">Select **Update**.</span></span> <span data-ttu-id="b1030-122">The list should refresh accordingly.</span><span class="sxs-lookup"><span data-stu-id="b1030-122">The list should refresh accordingly.</span></span>
   
    ![](media/azure-stack-manage-storage-accounts/image5.png)
4. <span data-ttu-id="b1030-123">To reset the filter: select **Filter**, clear out the  selections and update.</span><span class="sxs-lookup"><span data-stu-id="b1030-123">To reset the filter: select **Filter**, clear out the  selections and update.</span></span>

<span data-ttu-id="b1030-124">The search text box (on the top of the storage accounts list pane) lets you highlight the selected text in the list of accounts.</span><span class="sxs-lookup"><span data-stu-id="b1030-124">The search text box (on the top of the storage accounts list pane) lets you highlight the selected text in the list of accounts.</span></span> <span data-ttu-id="b1030-125">You can use this when the full name or ID is not easily available.</span><span class="sxs-lookup"><span data-stu-id="b1030-125">You can use this when the full name or ID is not easily available.</span></span>

<span data-ttu-id="b1030-126">You can use free text here to help find the account you are interested in.</span><span class="sxs-lookup"><span data-stu-id="b1030-126">You can use free text here to help find the account you are interested in.</span></span>

![](media/azure-stack-manage-storage-accounts/image6.png)

## <a name="look-at-account-details"></a><span data-ttu-id="b1030-127">Look at account details</span><span class="sxs-lookup"><span data-stu-id="b1030-127">Look at account details</span></span>
<span data-ttu-id="b1030-128">Once you have located the accounts you are interested in viewing, you can select the particular account to view certain details.</span><span class="sxs-lookup"><span data-stu-id="b1030-128">Once you have located the accounts you are interested in viewing, you can select the particular account to view certain details.</span></span> <span data-ttu-id="b1030-129">A new pane opens with the account details such as: the type of the account, creation time, location, etc.</span><span class="sxs-lookup"><span data-stu-id="b1030-129">A new pane opens with the account details such as: the type of the account, creation time, location, etc.</span></span>

![](media/azure-stack-manage-storage-accounts/image7.png)

## <a name="recover-a-deleted-account"></a><span data-ttu-id="b1030-130">Recover a deleted account</span><span class="sxs-lookup"><span data-stu-id="b1030-130">Recover a deleted account</span></span>
<span data-ttu-id="b1030-131">You may be in a situation where you need to recover a deleted account.</span><span class="sxs-lookup"><span data-stu-id="b1030-131">You may be in a situation where you need to recover a deleted account.</span></span>

<span data-ttu-id="b1030-132">In Azure Stack there is a simple way to do that:</span><span class="sxs-lookup"><span data-stu-id="b1030-132">In Azure Stack there is a simple way to do that:</span></span>

1. <span data-ttu-id="b1030-133">Browse to the storage accounts list.</span><span class="sxs-lookup"><span data-stu-id="b1030-133">Browse to the storage accounts list.</span></span> <span data-ttu-id="b1030-134">See [Find a storage account](#find) in this topic for more information.</span><span class="sxs-lookup"><span data-stu-id="b1030-134">See [Find a storage account](#find) in this topic for more information.</span></span>
2. <span data-ttu-id="b1030-135">Locate that particular account in the list.</span><span class="sxs-lookup"><span data-stu-id="b1030-135">Locate that particular account in the list.</span></span> <span data-ttu-id="b1030-136">You may need to filter.</span><span class="sxs-lookup"><span data-stu-id="b1030-136">You may need to filter.</span></span>
3. <span data-ttu-id="b1030-137">Check the *state* of the account.</span><span class="sxs-lookup"><span data-stu-id="b1030-137">Check the *state* of the account.</span></span> <span data-ttu-id="b1030-138">It should say **Deleted**.</span><span class="sxs-lookup"><span data-stu-id="b1030-138">It should say **Deleted**.</span></span>
4. <span data-ttu-id="b1030-139">Select the account, which opens the account details pane.</span><span class="sxs-lookup"><span data-stu-id="b1030-139">Select the account, which opens the account details pane.</span></span>
5. <span data-ttu-id="b1030-140">On top of this pane, locate the **Recover** button and select it.</span><span class="sxs-lookup"><span data-stu-id="b1030-140">On top of this pane, locate the **Recover** button and select it.</span></span>
6. <span data-ttu-id="b1030-141">Select **Yes** to confirm.</span><span class="sxs-lookup"><span data-stu-id="b1030-141">Select **Yes** to confirm.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image8.png)
7. <span data-ttu-id="b1030-142">The recovery is now in *process…wait* for an indication that it was successful.</span><span class="sxs-lookup"><span data-stu-id="b1030-142">The recovery is now in *process…wait* for an indication that it was successful.</span></span>
   <span data-ttu-id="b1030-143">You can also select the “bell” icon at the top of the portal to view progress indications.</span><span class="sxs-lookup"><span data-stu-id="b1030-143">You can also select the “bell” icon at the top of the portal to view progress indications.</span></span>
   
   ![](media/azure-stack-manage-storage-accounts/image9.png)
   
   <span data-ttu-id="b1030-144">Once the recovered account is successfully synchronized, it can be used again.</span><span class="sxs-lookup"><span data-stu-id="b1030-144">Once the recovered account is successfully synchronized, it can be used again.</span></span>

### <a name="some-gotchas"></a><span data-ttu-id="b1030-145">Some Gotchas</span><span class="sxs-lookup"><span data-stu-id="b1030-145">Some Gotchas</span></span>
* <span data-ttu-id="b1030-146">Your deleted account shows state as **out of retention**.</span><span class="sxs-lookup"><span data-stu-id="b1030-146">Your deleted account shows state as **out of retention**.</span></span>
  
  <span data-ttu-id="b1030-147">Out of retention means that the deleted account has exceeded the retention period and may not be recoverable.</span><span class="sxs-lookup"><span data-stu-id="b1030-147">Out of retention means that the deleted account has exceeded the retention period and may not be recoverable.</span></span>
* <span data-ttu-id="b1030-148">Your deleted account does not show in the accounts list.</span><span class="sxs-lookup"><span data-stu-id="b1030-148">Your deleted account does not show in the accounts list.</span></span>
  
  <span data-ttu-id="b1030-149">You account may not show in the account list when the deleted account has already been garbage collected.</span><span class="sxs-lookup"><span data-stu-id="b1030-149">You account may not show in the account list when the deleted account has already been garbage collected.</span></span> <span data-ttu-id="b1030-150">In this case, it cannot be recovered.</span><span class="sxs-lookup"><span data-stu-id="b1030-150">In this case, it cannot be recovered.</span></span> <span data-ttu-id="b1030-151">See [Reclaim capacity](#reclaim) in this topic.</span><span class="sxs-lookup"><span data-stu-id="b1030-151">See [Reclaim capacity](#reclaim) in this topic.</span></span>

## <a name="set-the-retention-period"></a><span data-ttu-id="b1030-152">Set the retention period</span><span class="sxs-lookup"><span data-stu-id="b1030-152">Set the retention period</span></span>
<span data-ttu-id="b1030-153">The retention period setting allows a cloud operator to specify a time period in days (between 0 and 9999 days) during which any deleted account can potentially be recovered.</span><span class="sxs-lookup"><span data-stu-id="b1030-153">The retention period setting allows a cloud operator to specify a time period in days (between 0 and 9999 days) during which any deleted account can potentially be recovered.</span></span> <span data-ttu-id="b1030-154">The default retention period is set to 0 days.</span><span class="sxs-lookup"><span data-stu-id="b1030-154">The default retention period is set to 0 days.</span></span> <span data-ttu-id="b1030-155">Setting the value to “0” means that any deleted account is immediately out of retention and marked for periodic garbage collection.</span><span class="sxs-lookup"><span data-stu-id="b1030-155">Setting the value to “0” means that any deleted account is immediately out of retention and marked for periodic garbage collection.</span></span>

<span data-ttu-id="b1030-156">**To change the retention period:**</span><span class="sxs-lookup"><span data-stu-id="b1030-156">**To change the retention period:**</span></span>

1. <span data-ttu-id="b1030-157">In an internet browser, navigate to https://adminportal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="b1030-157">In an internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="b1030-158">Sign in to the Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span><span class="sxs-lookup"><span data-stu-id="b1030-158">Sign in to the Azure Stack administration portal as a cloud operator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="b1030-159">On the default dashboard – find the **Region management** list and select the region you want to explore – for example **(local**).</span><span class="sxs-lookup"><span data-stu-id="b1030-159">On the default dashboard – find the **Region management** list and select the region you want to explore – for example **(local**).</span></span>
4. <span data-ttu-id="b1030-160">Select **Storage** from the **Resource Providers** list.</span><span class="sxs-lookup"><span data-stu-id="b1030-160">Select **Storage** from the **Resource Providers** list.</span></span>
5. <span data-ttu-id="b1030-161">Select **Settings** at the top to open the setting pane.</span><span class="sxs-lookup"><span data-stu-id="b1030-161">Select **Settings** at the top to open the setting pane.</span></span>
6. <span data-ttu-id="b1030-162">Select **Configuration** then edit the retention period value.</span><span class="sxs-lookup"><span data-stu-id="b1030-162">Select **Configuration** then edit the retention period value.</span></span>

   <span data-ttu-id="b1030-163">Set the number of days and then save it.</span><span class="sxs-lookup"><span data-stu-id="b1030-163">Set the number of days and then save it.</span></span>
   
   <span data-ttu-id="b1030-164">This value is immediately effective and is set for your entire region.</span><span class="sxs-lookup"><span data-stu-id="b1030-164">This value is immediately effective and is set for your entire region.</span></span>

   ![](media/azure-stack-manage-storage-accounts/image10.png)

## <a name="reclaim"></a><span data-ttu-id="b1030-165">Reclaim capacity</span><span class="sxs-lookup"><span data-stu-id="b1030-165">Reclaim capacity</span></span>
<span data-ttu-id="b1030-166">One of the side effects of having a retention period is that a deleted account continues to consume capacity until it comes out of the retention period.</span><span class="sxs-lookup"><span data-stu-id="b1030-166">One of the side effects of having a retention period is that a deleted account continues to consume capacity until it comes out of the retention period.</span></span> <span data-ttu-id="b1030-167">As a cloud operator you may need a way to reclaim the deleted account space even though the retention period has not yet expired.</span><span class="sxs-lookup"><span data-stu-id="b1030-167">As a cloud operator you may need a way to reclaim the deleted account space even though the retention period has not yet expired.</span></span>

<span data-ttu-id="b1030-168">You can reclaim capacity using either the portal or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b1030-168">You can reclaim capacity using either the portal or PowerShell.</span></span>

<span data-ttu-id="b1030-169">**To reclaim capacity using the portal:**</span><span class="sxs-lookup"><span data-stu-id="b1030-169">**To reclaim capacity using the portal:**</span></span>
1. <span data-ttu-id="b1030-170">Navigate to the storage accounts pane.</span><span class="sxs-lookup"><span data-stu-id="b1030-170">Navigate to the storage accounts pane.</span></span> <span data-ttu-id="b1030-171">See [Find a storage account](#find).</span><span class="sxs-lookup"><span data-stu-id="b1030-171">See [Find a storage account](#find).</span></span>
2. <span data-ttu-id="b1030-172">Select **Reclaim space** at the top of the pane.</span><span class="sxs-lookup"><span data-stu-id="b1030-172">Select **Reclaim space** at the top of the pane.</span></span>
3. <span data-ttu-id="b1030-173">Read the message and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1030-173">Read the message and then select **OK**.</span></span>

    ![](media/azure-stack-manage-storage-accounts/image11.png)
4. <span data-ttu-id="b1030-174">Wait for success notification See the bell icon on the portal.</span><span class="sxs-lookup"><span data-stu-id="b1030-174">Wait for success notification See the bell icon on the portal.</span></span>

    ![](media/azure-stack-manage-storage-accounts/image12.png)
5. <span data-ttu-id="b1030-175">Refresh the Storage accounts page.</span><span class="sxs-lookup"><span data-stu-id="b1030-175">Refresh the Storage accounts page.</span></span> <span data-ttu-id="b1030-176">The deleted accounts are no longer shown in the list because they have been purged.</span><span class="sxs-lookup"><span data-stu-id="b1030-176">The deleted accounts are no longer shown in the list because they have been purged.</span></span>

<span data-ttu-id="b1030-177">You can also use PowerShell to explicitly override the retention period and immediately reclaim capacity.</span><span class="sxs-lookup"><span data-stu-id="b1030-177">You can also use PowerShell to explicitly override the retention period and immediately reclaim capacity.</span></span>

<span data-ttu-id="b1030-178">**To reclaim capacity using PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="b1030-178">**To reclaim capacity using PowerShell:**</span></span>   

1. <span data-ttu-id="b1030-179">Confirm that you have Azure PowerShell installed and configured.</span><span class="sxs-lookup"><span data-stu-id="b1030-179">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="b1030-180">If not, use the following instructions:</span><span class="sxs-lookup"><span data-stu-id="b1030-180">If not, use the following instructions:</span></span> 
   * <span data-ttu-id="b1030-181">To install the latest Azure PowerShell version and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="b1030-181">To install the latest Azure PowerShell version and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
   <span data-ttu-id="b1030-182">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span><span class="sxs-lookup"><span data-stu-id="b1030-182">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="b1030-183">Run the following cmdlets:</span><span class="sxs-lookup"><span data-stu-id="b1030-183">Run the following cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="b1030-184">If you run these cmdlets, you permanently delete the account and its contents.</span><span class="sxs-lookup"><span data-stu-id="b1030-184">If you run these cmdlets, you permanently delete the account and its contents.</span></span> <span data-ttu-id="b1030-185">It is not recoverable.</span><span class="sxs-lookup"><span data-stu-id="b1030-185">It is not recoverable.</span></span> <span data-ttu-id="b1030-186">Use this with care.</span><span class="sxs-lookup"><span data-stu-id="b1030-186">Use this with care.</span></span>

```PowerShell  
    $farm_name = (Get-AzsStorageFarm)[0].name
    Start-AzsReclaimStorageCapacity -FarmName $farm_name
````

<span data-ttu-id="b1030-187">For more information, see [Azure Stack PowerShell documentation.](https://docs.microsoft.com/powershell/module/azurerm.azurestackstorage)</span><span class="sxs-lookup"><span data-stu-id="b1030-187">For more information, see [Azure Stack PowerShell documentation.](https://docs.microsoft.com/powershell/module/azurerm.azurestackstorage)</span></span>
 

## <a name="next-steps"></a><span data-ttu-id="b1030-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="b1030-188">Next steps</span></span>

 - <span data-ttu-id="b1030-189">For information on managing permissions see [Manage Role-Based Access Control](azure-stack-manage-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="b1030-189">For information on managing permissions see [Manage Role-Based Access Control](azure-stack-manage-permissions.md).</span></span>
 - <span data-ttu-id="b1030-190">For information on Manage storage capacity for Azure Stack, see [Manage storage capacity for Azure Stack](azure-stack-manage-storage-shares.md).</span><span class="sxs-lookup"><span data-stu-id="b1030-190">For information on Manage storage capacity for Azure Stack, see [Manage storage capacity for Azure Stack](azure-stack-manage-storage-shares.md).</span></span>