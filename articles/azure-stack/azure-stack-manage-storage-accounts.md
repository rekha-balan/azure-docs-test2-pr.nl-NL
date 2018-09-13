---
title: Manage Azure Stack storage accounts  | Microsoft Docs
description: Learn how to find, manage, recover and reclaim Azure Stack storage accounts
services: azure-stack
documentationcenter: ''
author: AniAnirudh
manager: darmour
editor: ''
ms.assetid: 627d355b-4812-45cb-bc1e-ce62476dab34
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/6/2017
ms.author: anirudha
ms.openlocfilehash: 9253145a14772816f0dbf09a223d5711601ba69c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669000"
---
# <a name="manage-storage-accounts-in-azure-stack"></a><span data-ttu-id="9c7fb-103">Manage Storage Accounts in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="9c7fb-103">Manage Storage Accounts in Azure Stack</span></span>
<span data-ttu-id="9c7fb-104">Learn how to manage storage accounts in Azure Stack to find, recover, and reclaim storage capacity based on business needs.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-104">Learn how to manage storage accounts in Azure Stack to find, recover, and reclaim storage capacity based on business needs.</span></span>

## <a name="find"></a><span data-ttu-id="9c7fb-105">Find a storage account</span><span class="sxs-lookup"><span data-stu-id="9c7fb-105">Find a storage account</span></span>
<span data-ttu-id="9c7fb-106">The list of storage accounts in the region can be viewed in Azure Stack by:</span><span class="sxs-lookup"><span data-stu-id="9c7fb-106">The list of storage accounts in the region can be viewed in Azure Stack by:</span></span>

1. <span data-ttu-id="9c7fb-107">In an Internet browser, navigate to https://adminportal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-107">In an Internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="9c7fb-108">Sign in to the Azure Stack administration portal as an administrator (using the credentials you provided during deployment)</span><span class="sxs-lookup"><span data-stu-id="9c7fb-108">Sign in to the Azure Stack administration portal as an administrator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="9c7fb-109">On the default dashboard – find the **Region management** list and click the region you want to explore.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-109">On the default dashboard – find the **Region management** list and click the region you want to explore.</span></span> <span data-ttu-id="9c7fb-110">For example **(local**).</span><span class="sxs-lookup"><span data-stu-id="9c7fb-110">For example **(local**).</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-storage-accounts/image1.png)
4. <span data-ttu-id="9c7fb-111">Select **Storage** from the **Resource Providers** list.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-111">Select **Storage** from the **Resource Providers** list.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-storage-accounts/image2.png)
5. <span data-ttu-id="9c7fb-112">Now, on the storage Resource Provider administrator blade – scroll down to the **Storage accounts** tab and click it.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-112">Now, on the storage Resource Provider administrator blade – scroll down to the **Storage accounts** tab and click it.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-storage-accounts/image3.png)
   
   <span data-ttu-id="9c7fb-113">The resulting page is the list of storage accounts in that region.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-113">The resulting page is the list of storage accounts in that region.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-storage-accounts/image4.png)

<span data-ttu-id="9c7fb-114">By default, the first 10 accounts are displayed.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-114">By default, the first 10 accounts are displayed.</span></span> <span data-ttu-id="9c7fb-115">You can choose to fetch more by clicking the  **Load more** link at the bottom of the list.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-115">You can choose to fetch more by clicking the  **Load more** link at the bottom of the list.</span></span>

<span data-ttu-id="9c7fb-116">OR</span><span class="sxs-lookup"><span data-stu-id="9c7fb-116">OR</span></span>

<span data-ttu-id="9c7fb-117">If you are interested in a particular storage account – you can **filter and fetch the relevant accounts** only.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-117">If you are interested in a particular storage account – you can **filter and fetch the relevant accounts** only.</span></span>


<span data-ttu-id="9c7fb-118">**To filter for accounts:**</span><span class="sxs-lookup"><span data-stu-id="9c7fb-118">**To filter for accounts:**</span></span>

1. <span data-ttu-id="9c7fb-119">Click **Filter** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-119">Click **Filter** at the top of the blade.</span></span>
2. <span data-ttu-id="9c7fb-120">On the Filter blade, it allows you to specify **account name**, **subscription ID** or **status** to fine-tune the list of storage accounts to be displayed.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-120">On the Filter blade, it allows you to specify **account name**, **subscription ID** or **status** to fine-tune the list of storage accounts to be displayed.</span></span> <span data-ttu-id="9c7fb-121">Use them as appropriate.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-121">Use them as appropriate.</span></span>
3. <span data-ttu-id="9c7fb-122">Click **Update**.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-122">Click **Update**.</span></span> <span data-ttu-id="9c7fb-123">The list should refresh accordingly.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-123">The list should refresh accordingly.</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-storage-accounts/image5.png)
4. <span data-ttu-id="9c7fb-124">To reset the filter: click **Filter**, clear out the  selections and update.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-124">To reset the filter: click **Filter**, clear out the  selections and update.</span></span>

<span data-ttu-id="9c7fb-125">The search text box (on the top of the storage accounts list blade) lets you highlight the selected text in the list of accounts.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-125">The search text box (on the top of the storage accounts list blade) lets you highlight the selected text in the list of accounts.</span></span> <span data-ttu-id="9c7fb-126">This is really handy in the case when the full name or id is not easily available.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-126">This is really handy in the case when the full name or id is not easily available.</span></span>

<span data-ttu-id="9c7fb-127">You can use free text here to help find the account you are interested in.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-127">You can use free text here to help find the account you are interested in.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-storage-accounts/image6.png)

## <a name="look-at-account-details"></a><span data-ttu-id="9c7fb-128">Look at account details</span><span class="sxs-lookup"><span data-stu-id="9c7fb-128">Look at account details</span></span>
<span data-ttu-id="9c7fb-129">Once you have located the accounts you are interested in viewing, you can click the particular account to view certain details.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-129">Once you have located the accounts you are interested in viewing, you can click the particular account to view certain details.</span></span> <span data-ttu-id="9c7fb-130">A new blade opens with the account details such as: the type of the account, creation time, location, etc.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-130">A new blade opens with the account details such as: the type of the account, creation time, location, etc.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-storage-accounts/image7.png)

## <a name="recover-a-deleted-account"></a><span data-ttu-id="9c7fb-131">Recover a deleted account</span><span class="sxs-lookup"><span data-stu-id="9c7fb-131">Recover a deleted account</span></span>
<span data-ttu-id="9c7fb-132">You may be in a situation where you need to recover a deleted account.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-132">You may be in a situation where you need to recover a deleted account.</span></span>

<span data-ttu-id="9c7fb-133">In Azure Stack there is a very simple way to do that:</span><span class="sxs-lookup"><span data-stu-id="9c7fb-133">In Azure Stack there is a very simple way to do that:</span></span>

1. <span data-ttu-id="9c7fb-134">Browse to the storage accounts list.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-134">Browse to the storage accounts list.</span></span> <span data-ttu-id="9c7fb-135">See [Find a storage account](#find) in this topic for more information.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-135">See [Find a storage account](#find) in this topic for more information.</span></span>
2. <span data-ttu-id="9c7fb-136">Locate that particular account in the list.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-136">Locate that particular account in the list.</span></span> <span data-ttu-id="9c7fb-137">You may need to filter.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-137">You may need to filter.</span></span>
3. <span data-ttu-id="9c7fb-138">Check the *state* of the account.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-138">Check the *state* of the account.</span></span> <span data-ttu-id="9c7fb-139">It should say **Deleted**.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-139">It should say **Deleted**.</span></span>
4. <span data-ttu-id="9c7fb-140">Click the account which opens the account details blade.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-140">Click the account which opens the account details blade.</span></span>
5. <span data-ttu-id="9c7fb-141">On top of this blade, locate the **Recover** button and click it.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-141">On top of this blade, locate the **Recover** button and click it.</span></span>
6. <span data-ttu-id="9c7fb-142">Click **Yes** to confirm.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-142">Click **Yes** to confirm.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-storage-accounts/image8.png)
7. <span data-ttu-id="9c7fb-143">The recovery is now in *process…wait* for an indication that it was successful.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-143">The recovery is now in *process…wait* for an indication that it was successful.</span></span>
   <span data-ttu-id="9c7fb-144">You can also click the “bell” icon at the top of the portal to view progress indications.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-144">You can also click the “bell” icon at the top of the portal to view progress indications.</span></span>
   
   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-storage-accounts/image9.png)
   
   <span data-ttu-id="9c7fb-145">Once the recovered account is successfully synchronized, it can be used again.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-145">Once the recovered account is successfully synchronized, it can be used again.</span></span>

### <a name="some-gotchas"></a><span data-ttu-id="9c7fb-146">Some Gotchas</span><span class="sxs-lookup"><span data-stu-id="9c7fb-146">Some Gotchas</span></span>
* <span data-ttu-id="9c7fb-147">Your deleted account shows state as **out of retention**.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-147">Your deleted account shows state as **out of retention**.</span></span>
  
  <span data-ttu-id="9c7fb-148">This means that the deleted account has exceeded the retention period and may not be recoverable.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-148">This means that the deleted account has exceeded the retention period and may not be recoverable.</span></span>
* <span data-ttu-id="9c7fb-149">Your deleted account does not show in the accounts list.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-149">Your deleted account does not show in the accounts list.</span></span>
  
  <span data-ttu-id="9c7fb-150">This could mean that the deleted account has already been garbage collected.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-150">This could mean that the deleted account has already been garbage collected.</span></span> <span data-ttu-id="9c7fb-151">In this case it cannot be recovered.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-151">In this case it cannot be recovered.</span></span> <span data-ttu-id="9c7fb-152">See [Reclaim capacity](#reclaim) in this topic.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-152">See [Reclaim capacity](#reclaim) in this topic.</span></span>

## <a name="set-the-retention-period"></a><span data-ttu-id="9c7fb-153">Set the retention period</span><span class="sxs-lookup"><span data-stu-id="9c7fb-153">Set the retention period</span></span>
<span data-ttu-id="9c7fb-154">The retention period setting allows an administrator to specify a time period in days (between 0 and 9999 days) during which any deleted account can potentially be recovered.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-154">The retention period setting allows an administrator to specify a time period in days (between 0 and 9999 days) during which any deleted account can potentially be recovered.</span></span> <span data-ttu-id="9c7fb-155">The default retention period is set to 15 days.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-155">The default retention period is set to 15 days.</span></span> <span data-ttu-id="9c7fb-156">Setting the value to “0” means that any deleted account is immediately out of retention and marked for periodic garbage collection.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-156">Setting the value to “0” means that any deleted account is immediately out of retention and marked for periodic garbage collection.</span></span>

<span data-ttu-id="9c7fb-157">**To change the retention period:**</span><span class="sxs-lookup"><span data-stu-id="9c7fb-157">**To change the retention period:**</span></span>

1. <span data-ttu-id="9c7fb-158">In an internet browser, navigate to https://adminportal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-158">In an internet browser, navigate to https://adminportal.local.azurestack.external.</span></span>
2. <span data-ttu-id="9c7fb-159">Sign in to the Azure Stack administration portal as an administrator (using the credentials you provided during deployment)</span><span class="sxs-lookup"><span data-stu-id="9c7fb-159">Sign in to the Azure Stack administration portal as an administrator (using the credentials you provided during deployment)</span></span>
3. <span data-ttu-id="9c7fb-160">On the default dashboard – find the **Region management** list and click the region you want to explore – for example **(local**).</span><span class="sxs-lookup"><span data-stu-id="9c7fb-160">On the default dashboard – find the **Region management** list and click the region you want to explore – for example **(local**).</span></span>
4. <span data-ttu-id="9c7fb-161">Select **Storage** from the **Resource Providers** list.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-161">Select **Storage** from the **Resource Providers** list.</span></span>
5. <span data-ttu-id="9c7fb-162">Click **Settings** at the top to open the setting blade.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-162">Click **Settings** at the top to open the setting blade.</span></span>
6. <span data-ttu-id="9c7fb-163">Click **Configuration** then edit the retention period value.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-163">Click **Configuration** then edit the retention period value.</span></span>

   <span data-ttu-id="9c7fb-164">Set the number of days and then save it.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-164">Set the number of days and then save it.</span></span>
   
   <span data-ttu-id="9c7fb-165">This value is immediately effective and is set for your entire region.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-165">This value is immediately effective and is set for your entire region.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-storage-accounts/image10.png)

## <a name="reclaim"></a><span data-ttu-id="9c7fb-166">Reclaim capacity</span><span class="sxs-lookup"><span data-stu-id="9c7fb-166">Reclaim capacity</span></span>
<span data-ttu-id="9c7fb-167">One of the side effects of having a retention period is that a deleted account continues to consume capacity until it comes out of the retention period.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-167">One of the side effects of having a retention period is that a deleted account continues to consume capacity until it comes out of the retention period.</span></span> <span data-ttu-id="9c7fb-168">As an administrator you may need a way to reclaim the deleted account space even though the retention period has not yet expired.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-168">As an administrator you may need a way to reclaim the deleted account space even though the retention period has not yet expired.</span></span>

<span data-ttu-id="9c7fb-169">You can reclaim capacity using either the portal or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-169">You can reclaim capacity using either the portal or PowerShell.</span></span>

<span data-ttu-id="9c7fb-170">**To reclaim capacity using the portal:**</span><span class="sxs-lookup"><span data-stu-id="9c7fb-170">**To reclaim capacity using the portal:**</span></span>
1. <span data-ttu-id="9c7fb-171">Navigate to the storage accounts blade.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-171">Navigate to the storage accounts blade.</span></span> <span data-ttu-id="9c7fb-172">See [Find a storage account](#find).</span><span class="sxs-lookup"><span data-stu-id="9c7fb-172">See [Find a storage account](#find).</span></span>
2. <span data-ttu-id="9c7fb-173">Click **Reclaim space** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-173">Click **Reclaim space** at the top of the blade.</span></span>
3. <span data-ttu-id="9c7fb-174">Read the message and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-174">Read the message and then click **OK**.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-storage-accounts/image11.png)
4. <span data-ttu-id="9c7fb-175">Wait for success notification See the bell icon on the portal.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-175">Wait for success notification See the bell icon on the portal.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-storage-accounts/image12.png)
5. <span data-ttu-id="9c7fb-176">Refresh the Storage accounts page.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-176">Refresh the Storage accounts page.</span></span> <span data-ttu-id="9c7fb-177">The deleted accounts are no longer shown in the list because they have been purged.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-177">The deleted accounts are no longer shown in the list because they have been purged.</span></span>

<span data-ttu-id="9c7fb-178">You can also use PowerShell to explicitly override the retention period and immediately reclaim capacity.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-178">You can also use PowerShell to explicitly override the retention period and immediately reclaim capacity.</span></span>

<span data-ttu-id="9c7fb-179">**To reclaim capacity using PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="9c7fb-179">**To reclaim capacity using PowerShell:**</span></span>   

1. <span data-ttu-id="9c7fb-180">Confirm that you have Azure PowerShell installed and configured.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-180">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="9c7fb-181">If not, use the following instructions:</span><span class="sxs-lookup"><span data-stu-id="9c7fb-181">If not, use the following instructions:</span></span> 
   * <span data-ttu-id="9c7fb-182">To install the latest Azure PowerShell version and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="9c7fb-182">To install the latest Azure PowerShell version and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
   <span data-ttu-id="9c7fb-183">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span><span class="sxs-lookup"><span data-stu-id="9c7fb-183">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="9c7fb-184">Run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9c7fb-184">Run the following cmdlet:</span></span>

> [!NOTE]
> <span data-ttu-id="9c7fb-185">If you run this cmdlet you permanently delete the account and its contents.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-185">If you run this cmdlet you permanently delete the account and its contents.</span></span> <span data-ttu-id="9c7fb-186">It is not recoverable.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-186">It is not recoverable.</span></span> <span data-ttu-id="9c7fb-187">Use this with care.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-187">Use this with care.</span></span>


        Clear-ACSStorageAccount -ResourceGroupName system.local -FarmName <farm ID>


<span data-ttu-id="9c7fb-188">For more details, refer to [Azure Stack powershell documentation.](https://msdn.microsoft.com/library/mt637964.aspx)</span><span class="sxs-lookup"><span data-stu-id="9c7fb-188">For more details, refer to [Azure Stack powershell documentation.](https://msdn.microsoft.com/library/mt637964.aspx)</span></span>
 

## <a name="migrate-a-container"></a><span data-ttu-id="9c7fb-189">Migrate a container</span><span class="sxs-lookup"><span data-stu-id="9c7fb-189">Migrate a container</span></span>
<span data-ttu-id="9c7fb-190">Due to uneven storage use by tenants, an administrator may find one or more underlying tenant shares using more space than others.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-190">Due to uneven storage use by tenants, an administrator may find one or more underlying tenant shares using more space than others.</span></span> <span data-ttu-id="9c7fb-191">If this occurs, the administrator can attempt to free up some space on the stressed share by manually migrating some blob containers to another share.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-191">If this occurs, the administrator can attempt to free up some space on the stressed share by manually migrating some blob containers to another share.</span></span> 

<span data-ttu-id="9c7fb-192">You must use PowerShell to migrate containers.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-192">You must use PowerShell to migrate containers.</span></span>
> [!NOTE]
><span data-ttu-id="9c7fb-193">Blob container migration does not support live migration and currently is an offline operation.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-193">Blob container migration does not support live migration and currently is an offline operation.</span></span> <span data-ttu-id="9c7fb-194">During migration and until it is complete the underlying blobs in that container cannot be used and are “offline”.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-194">During migration and until it is complete the underlying blobs in that container cannot be used and are “offline”.</span></span> 

<span data-ttu-id="9c7fb-195">**To migrate containers using PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="9c7fb-195">**To migrate containers using PowerShell:**</span></span>

1. <span data-ttu-id="9c7fb-196">Confirm that you have Azure PowerShell installed and configured.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-196">Confirm that you have Azure PowerShell installed and configured.</span></span> <span data-ttu-id="9c7fb-197">If not, use the following instructions:</span><span class="sxs-lookup"><span data-stu-id="9c7fb-197">If not, use the following instructions:</span></span>
    * <span data-ttu-id="9c7fb-198">To install the latest Azure PowerShell version and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="9c7fb-198">To install the latest Azure PowerShell version and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span> <span data-ttu-id="9c7fb-199">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span><span class="sxs-lookup"><span data-stu-id="9c7fb-199">For more information about Azure Resource Manager cmdlets, see [Using Azure PowerShell with Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767)</span></span>
2. <span data-ttu-id="9c7fb-200">Get the farm name:</span><span class="sxs-lookup"><span data-stu-id="9c7fb-200">Get the farm name:</span></span> 
      
      `$farm = Get-ACSFarm -ResourceGroupName system.local`
3. <span data-ttu-id="9c7fb-201">Get the shares:</span><span class="sxs-lookup"><span data-stu-id="9c7fb-201">Get the shares:</span></span> 

   `$shares = Get-ACSShare -ResourceGroupName system.local -FarmName $farm.FarmName`

4. <span data-ttu-id="9c7fb-202">Get the containers for a given share.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-202">Get the containers for a given share.</span></span> <span data-ttu-id="9c7fb-203">Note that count and intent are optional parameters:</span><span class="sxs-lookup"><span data-stu-id="9c7fb-203">Note that count and intent are optional parameters:</span></span>
            
   `$containers = Get-ACSContainer -ResourceGroupName system.local -FarmName $farm.FarmName -ShareName $shares[0].ShareName -Count 4 -Intent Migration`  

   <span data-ttu-id="9c7fb-204">Then examine $containers:</span><span class="sxs-lookup"><span data-stu-id="9c7fb-204">Then examine $containers:</span></span>

   `$containers`

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-storage-accounts/image13.png)
5. <span data-ttu-id="9c7fb-205">Get the best destination shares for the container migration:</span><span class="sxs-lookup"><span data-stu-id="9c7fb-205">Get the best destination shares for the container migration:</span></span>

    `$destinationshares= Get-ACSSharesForMigration  -ResourceGroupName system.local -FarmName $farm.farmname -SourceShareName $shares[0].ShareName`

    <span data-ttu-id="9c7fb-206">Then examine $destinationshares:</span><span class="sxs-lookup"><span data-stu-id="9c7fb-206">Then examine $destinationshares:</span></span>

    `$destinationshares`

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-storage-accounts/image14.png)
6. <span data-ttu-id="9c7fb-207">Kick off migration for a container, notice this is an async implementation, so one can loop all containers in a share and track the status using the returned job id.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-207">Kick off migration for a container, notice this is an async implementation, so one can loop all containers in a share and track the status using the returned job id.</span></span>

    `$jobId = Start-ACSContainerMigration -ResourceGroupName system.local -FarmName $farm.farmname -ContainerToMigrate $containers[1] -DestinationShareUncPath $destinationshares.UncPath`

    <span data-ttu-id="9c7fb-208">Then examine $jobId:</span><span class="sxs-lookup"><span data-stu-id="9c7fb-208">Then examine $jobId:</span></span>

   ```
   $jobId
   d1d5277f-6b8d-4923-9db3-8bb00fa61b65
   ```
7. <span data-ttu-id="9c7fb-209">Check status of the migration job by its job id. When the container migration finishes, MigrationStatus is set to “Completed”.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-209">Check status of the migration job by its job id. When the container migration finishes, MigrationStatus is set to “Completed”.</span></span>

    `Get-ACSContainerMigrationStatus -ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-storage-accounts/image15.png)

8. <span data-ttu-id="9c7fb-210">You can cancel an in-progress migration job.</span><span class="sxs-lookup"><span data-stu-id="9c7fb-210">You can cancel an in-progress migration job.</span></span> <span data-ttu-id="9c7fb-211">This again is an async operation and can be tracked using $jobid:</span><span class="sxs-lookup"><span data-stu-id="9c7fb-211">This again is an async operation and can be tracked using $jobid:</span></span>

    `Stop-ACSContainerMigration-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId-Verbose`

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-storage-accounts/image16.png)

    <span data-ttu-id="9c7fb-212">You can check the status of the migration cancel again:</span><span class="sxs-lookup"><span data-stu-id="9c7fb-212">You can check the status of the migration cancel again:</span></span>

    `Get-ACSContainerMigrationStatus-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-storage-accounts/image17.png)




  
  
















