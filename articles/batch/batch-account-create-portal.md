---
title: Create a Batch account in the Azure portal | Microsoft Docs
description: Learn how to create an Azure Batch account in the Azure portal to run large-scale parallel workloads in the cloud
services: batch
documentationcenter: ''
author: tamram
manager: timlt
editor: ''
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 239aeb2239f34868eb95067076a2dc4d56c36803
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662994"
---
# <a name="create-a-batch-account-with-the-azure-portal"></a><span data-ttu-id="d85ce-103">Create a Batch account with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d85ce-103">Create a Batch account with the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](batch-account-create-portal.md)
> * [Batch Management .NET](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="d85ce-106">Learn how to create an Azure Batch account in the [Azure portal][azure_portal], and choose the account properties that fit your compute scenario.</span><span class="sxs-lookup"><span data-stu-id="d85ce-106">Learn how to create an Azure Batch account in the [Azure portal][azure_portal], and choose the account properties that fit your compute scenario.</span></span> <span data-ttu-id="d85ce-107">Learn where to find important account properties like access keys and account URLs.</span><span class="sxs-lookup"><span data-stu-id="d85ce-107">Learn where to find important account properties like access keys and account URLs.</span></span> 

<span data-ttu-id="d85ce-108">For background about Batch accounts and scenarios, see the [feature overview](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="d85ce-108">For background about Batch accounts and scenarios, see the [feature overview](batch-api-basics.md).</span></span>



## <a name="create-a-batch-account"></a><span data-ttu-id="d85ce-109">Create a Batch account</span><span class="sxs-lookup"><span data-stu-id="d85ce-109">Create a Batch account</span></span>

<span data-ttu-id="d85ce-110">Use the portal to create a Batch account in one of the two *pool allocation modes*: **Batch service** mode or the newer **user subscription** mode, which requires more configuration.</span><span class="sxs-lookup"><span data-stu-id="d85ce-110">Use the portal to create a Batch account in one of the two *pool allocation modes*: **Batch service** mode or the newer **user subscription** mode, which requires more configuration.</span></span> <span data-ttu-id="d85ce-111">For information about these two modes, see the [feature overview](batch-api-basics.md#account).</span><span class="sxs-lookup"><span data-stu-id="d85ce-111">For information about these two modes, see the [feature overview](batch-api-basics.md#account).</span></span> <span data-ttu-id="d85ce-112">For features of the user subscription mode, see also the [blog post](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span><span class="sxs-lookup"><span data-stu-id="d85ce-112">For features of the user subscription mode, see also the [blog post](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).</span></span>

## <a name="batch-service-mode"></a><span data-ttu-id="d85ce-113">Batch service mode</span><span class="sxs-lookup"><span data-stu-id="d85ce-113">Batch service mode</span></span>



1. <span data-ttu-id="d85ce-114">Sign in to the [Azure portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="d85ce-114">Sign in to the [Azure portal][azure_portal].</span></span>
2. <span data-ttu-id="d85ce-115">Click **New** > **Compute** > **Batch Service**.</span><span class="sxs-lookup"><span data-stu-id="d85ce-115">Click **New** > **Compute** > **Batch Service**.</span></span>
   
    ![Batch in the Marketplace][marketplace_portal]
3. <span data-ttu-id="d85ce-117">The **New Batch Account** blade is displayed.</span><span class="sxs-lookup"><span data-stu-id="d85ce-117">The **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="d85ce-118">See the descriptions below of each blade element.</span><span class="sxs-lookup"><span data-stu-id="d85ce-118">See the descriptions below of each blade element.</span></span>
   
    ![Create a Batch account][account_portal]
   
    <span data-ttu-id="d85ce-120">a.</span><span class="sxs-lookup"><span data-stu-id="d85ce-120">a.</span></span> <span data-ttu-id="d85ce-121">**Account name**: The Batch account name you choose must be unique within the Azure region where the account is created (see **Location** below).</span><span class="sxs-lookup"><span data-stu-id="d85ce-121">**Account name**: The Batch account name you choose must be unique within the Azure region where the account is created (see **Location** below).</span></span> <span data-ttu-id="d85ce-122">The account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span><span class="sxs-lookup"><span data-stu-id="d85ce-122">The account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>
   
    <span data-ttu-id="d85ce-123">b.</span><span class="sxs-lookup"><span data-stu-id="d85ce-123">b.</span></span> <span data-ttu-id="d85ce-124">**Subscription**: The subscription in which to create the Batch account.</span><span class="sxs-lookup"><span data-stu-id="d85ce-124">**Subscription**: The subscription in which to create the Batch account.</span></span> <span data-ttu-id="d85ce-125">If you have only one subscription, it is selected by default.</span><span class="sxs-lookup"><span data-stu-id="d85ce-125">If you have only one subscription, it is selected by default.</span></span>

    <span data-ttu-id="d85ce-126">c.</span><span class="sxs-lookup"><span data-stu-id="d85ce-126">c.</span></span> <span data-ttu-id="d85ce-127">**Pool allocation mode**: Select **Batch service**.</span><span class="sxs-lookup"><span data-stu-id="d85ce-127">**Pool allocation mode**: Select **Batch service**.</span></span>
   
    <span data-ttu-id="d85ce-128">c.</span><span class="sxs-lookup"><span data-stu-id="d85ce-128">c.</span></span> <span data-ttu-id="d85ce-129">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span><span class="sxs-lookup"><span data-stu-id="d85ce-129">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span></span>
   
    <span data-ttu-id="d85ce-130">d.</span><span class="sxs-lookup"><span data-stu-id="d85ce-130">d.</span></span> <span data-ttu-id="d85ce-131">**Location**: The Azure region in which to create the Batch account.</span><span class="sxs-lookup"><span data-stu-id="d85ce-131">**Location**: The Azure region in which to create the Batch account.</span></span> <span data-ttu-id="d85ce-132">Only the regions supported by your subscription and resource group are displayed as options.</span><span class="sxs-lookup"><span data-stu-id="d85ce-132">Only the regions supported by your subscription and resource group are displayed as options.</span></span>
   
    <span data-ttu-id="d85ce-133">e.</span><span class="sxs-lookup"><span data-stu-id="d85ce-133">e.</span></span> <span data-ttu-id="d85ce-134">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span><span class="sxs-lookup"><span data-stu-id="d85ce-134">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="d85ce-135">This is recommended for most Batch accounts.</span><span class="sxs-lookup"><span data-stu-id="d85ce-135">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="d85ce-136">See [Linked Azure Storage account](#linked-azure-storage-account) later in this article for more details.</span><span class="sxs-lookup"><span data-stu-id="d85ce-136">See [Linked Azure Storage account](#linked-azure-storage-account) later in this article for more details.</span></span>

4. <span data-ttu-id="d85ce-137">Click **Create** to create the account.</span><span class="sxs-lookup"><span data-stu-id="d85ce-137">Click **Create** to create the account.</span></span>
   
   <span data-ttu-id="d85ce-138">The portal indicates deployment is in progress.</span><span class="sxs-lookup"><span data-stu-id="d85ce-138">The portal indicates deployment is in progress.</span></span> <span data-ttu-id="d85ce-139">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span><span class="sxs-lookup"><span data-stu-id="d85ce-139">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>
   
## <a name="user-subscription-mode"></a><span data-ttu-id="d85ce-140">User subscription mode</span><span class="sxs-lookup"><span data-stu-id="d85ce-140">User subscription mode</span></span>

### <a name="allow-azure-batch-to-access-the-subscription-one-time-operation"></a><span data-ttu-id="d85ce-141">Allow Azure Batch to access the subscription (one-time operation)</span><span class="sxs-lookup"><span data-stu-id="d85ce-141">Allow Azure Batch to access the subscription (one-time operation)</span></span>
<span data-ttu-id="d85ce-142">When creating your first Batch account in user subscription mode, perform the following steps to register your subscription with Batch.</span><span class="sxs-lookup"><span data-stu-id="d85ce-142">When creating your first Batch account in user subscription mode, perform the following steps to register your subscription with Batch.</span></span> <span data-ttu-id="d85ce-143">(If you previously did this, skip to the next section.)</span><span class="sxs-lookup"><span data-stu-id="d85ce-143">(If you previously did this, skip to the next section.)</span></span>

1. <span data-ttu-id="d85ce-144">Sign in to the [Azure portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="d85ce-144">Sign in to the [Azure portal][azure_portal].</span></span>

2. <span data-ttu-id="d85ce-145">Click **More Services** > **Subscriptions**, and click the subscription you want to use for the Batch account.</span><span class="sxs-lookup"><span data-stu-id="d85ce-145">Click **More Services** > **Subscriptions**, and click the subscription you want to use for the Batch account.</span></span> 

3. <span data-ttu-id="d85ce-146">In the **Subscription** blade, click **Access control (IAM)** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="d85ce-146">In the **Subscription** blade, click **Access control (IAM)** > **Add**.</span></span>

    ![Subscription access control][subscription_access]

4. <span data-ttu-id="d85ce-148">On the **Add permissions** blade, select the **Contributor** role, and search for **MicrosoftAzureBatch** (no spaces).</span><span class="sxs-lookup"><span data-stu-id="d85ce-148">On the **Add permissions** blade, select the **Contributor** role, and search for **MicrosoftAzureBatch** (no spaces).</span></span> <span data-ttu-id="d85ce-149">Select **MicrosoftAzureBatch**, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d85ce-149">Select **MicrosoftAzureBatch**, and click **Save**.</span></span>

    ![Add Batch permissions][add_permission]

### <a name="create-a-key-vault"></a><span data-ttu-id="d85ce-151">Create a key vault</span><span class="sxs-lookup"><span data-stu-id="d85ce-151">Create a key vault</span></span>
<span data-ttu-id="d85ce-152">In user subscription mode, an Azure key vault is required that belongs to the same resource group as the Batch account to be created.</span><span class="sxs-lookup"><span data-stu-id="d85ce-152">In user subscription mode, an Azure key vault is required that belongs to the same resource group as the Batch account to be created.</span></span> <span data-ttu-id="d85ce-153">Make sure the resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span><span class="sxs-lookup"><span data-stu-id="d85ce-153">Make sure the resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span></span>

1. <span data-ttu-id="d85ce-154">In the [Azure portal][azure_portal], click **New** > **Security + Identity** > **Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="d85ce-154">In the [Azure portal][azure_portal], click **New** > **Security + Identity** > **Key Vault**.</span></span> 

2. <span data-ttu-id="d85ce-155">In the **Create Key Vault** blade, enter a name for the key vault, and create a resource group in the region you want for your Batch account.</span><span class="sxs-lookup"><span data-stu-id="d85ce-155">In the **Create Key Vault** blade, enter a name for the key vault, and create a resource group in the region you want for your Batch account.</span></span> <span data-ttu-id="d85ce-156">Leave the remaining settings at default values, then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d85ce-156">Leave the remaining settings at default values, then click **Create**.</span></span>

### <a name="create-a-batch-account"></a><span data-ttu-id="d85ce-157">Create a Batch account</span><span class="sxs-lookup"><span data-stu-id="d85ce-157">Create a Batch account</span></span>

1. <span data-ttu-id="d85ce-158">In the [Azure portal][azure_portal], click **New** > **Compute** > **Batch Service**.</span><span class="sxs-lookup"><span data-stu-id="d85ce-158">In the [Azure portal][azure_portal], click **New** > **Compute** > **Batch Service**.</span></span>
   
    ![Batch in the Marketplace][marketplace_portal]
3. <span data-ttu-id="d85ce-160">The **New Batch Account** blade is displayed.</span><span class="sxs-lookup"><span data-stu-id="d85ce-160">The **New Batch Account** blade is displayed.</span></span> <span data-ttu-id="d85ce-161">See the descriptions below of each blade element.</span><span class="sxs-lookup"><span data-stu-id="d85ce-161">See the descriptions below of each blade element.</span></span>
   
    ![Create a Batch account][account_portal_byos]
   
    <span data-ttu-id="d85ce-163">a.</span><span class="sxs-lookup"><span data-stu-id="d85ce-163">a.</span></span> <span data-ttu-id="d85ce-164">**Account name**: The Batch account name you choose must be unique within the Azure region where the account is created (see **Location** below).</span><span class="sxs-lookup"><span data-stu-id="d85ce-164">**Account name**: The Batch account name you choose must be unique within the Azure region where the account is created (see **Location** below).</span></span> <span data-ttu-id="d85ce-165">The account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span><span class="sxs-lookup"><span data-stu-id="d85ce-165">The account name may contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>
   
    <span data-ttu-id="d85ce-166">b.</span><span class="sxs-lookup"><span data-stu-id="d85ce-166">b.</span></span> <span data-ttu-id="d85ce-167">**Subscription**: If you have more than one subscription, select the subscription that you registered with the Batch service.</span><span class="sxs-lookup"><span data-stu-id="d85ce-167">**Subscription**: If you have more than one subscription, select the subscription that you registered with the Batch service.</span></span>

    <span data-ttu-id="d85ce-168">c.</span><span class="sxs-lookup"><span data-stu-id="d85ce-168">c.</span></span> <span data-ttu-id="d85ce-169">**Pool allocation mode**: Select **User subscription**.</span><span class="sxs-lookup"><span data-stu-id="d85ce-169">**Pool allocation mode**: Select **User subscription**.</span></span>

    <span data-ttu-id="d85ce-170">d.</span><span class="sxs-lookup"><span data-stu-id="d85ce-170">d.</span></span> <span data-ttu-id="d85ce-171">**Key vault**: Select the key vault you created for your Batch account in the previous section.</span><span class="sxs-lookup"><span data-stu-id="d85ce-171">**Key vault**: Select the key vault you created for your Batch account in the previous section.</span></span> <span data-ttu-id="d85ce-172">Optionally, create a new key vault.</span><span class="sxs-lookup"><span data-stu-id="d85ce-172">Optionally, create a new key vault.</span></span> <span data-ttu-id="d85ce-173">After selecting the vault, select the checkbox to grant Azure Batch access to the key vault.</span><span class="sxs-lookup"><span data-stu-id="d85ce-173">After selecting the vault, select the checkbox to grant Azure Batch access to the key vault.</span></span>
   
    <span data-ttu-id="d85ce-174">c.</span><span class="sxs-lookup"><span data-stu-id="d85ce-174">c.</span></span> <span data-ttu-id="d85ce-175">**Resource group**: Select the resource group in which you  created the key vault.</span><span class="sxs-lookup"><span data-stu-id="d85ce-175">**Resource group**: Select the resource group in which you  created the key vault.</span></span>
   
    <span data-ttu-id="d85ce-176">d.</span><span class="sxs-lookup"><span data-stu-id="d85ce-176">d.</span></span> <span data-ttu-id="d85ce-177">**Location**: The Azure region in which you created the key vault for the Batch account.</span><span class="sxs-lookup"><span data-stu-id="d85ce-177">**Location**: The Azure region in which you created the key vault for the Batch account.</span></span> 
   
    <span data-ttu-id="d85ce-178">e.</span><span class="sxs-lookup"><span data-stu-id="d85ce-178">e.</span></span> <span data-ttu-id="d85ce-179">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span><span class="sxs-lookup"><span data-stu-id="d85ce-179">**Storage account** (optional): A general-purpose Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="d85ce-180">This is recommended for most Batch accounts.</span><span class="sxs-lookup"><span data-stu-id="d85ce-180">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="d85ce-181">See [Linked Azure Storage account](#linked-azure-storage-account) below for more details.</span><span class="sxs-lookup"><span data-stu-id="d85ce-181">See [Linked Azure Storage account](#linked-azure-storage-account) below for more details.</span></span>

4. <span data-ttu-id="d85ce-182">Click **Create** to create the account.</span><span class="sxs-lookup"><span data-stu-id="d85ce-182">Click **Create** to create the account.</span></span>
   
   <span data-ttu-id="d85ce-183">The portal indicates deployment is in progress.</span><span class="sxs-lookup"><span data-stu-id="d85ce-183">The portal indicates deployment is in progress.</span></span> <span data-ttu-id="d85ce-184">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span><span class="sxs-lookup"><span data-stu-id="d85ce-184">Upon completion, a **Deployments succeeded** notification appears in **Notifications**.</span></span>



## <a name="view-batch-account-properties"></a><span data-ttu-id="d85ce-185">View Batch account properties</span><span class="sxs-lookup"><span data-stu-id="d85ce-185">View Batch account properties</span></span>
<span data-ttu-id="d85ce-186">Once the account has been created, you can open the **Batch account blade** to access its settings and properties.</span><span class="sxs-lookup"><span data-stu-id="d85ce-186">Once the account has been created, you can open the **Batch account blade** to access its settings and properties.</span></span> <span data-ttu-id="d85ce-187">You can access all account settings and properties by using the left menu of the Batch account blade.</span><span class="sxs-lookup"><span data-stu-id="d85ce-187">You can access all account settings and properties by using the left menu of the Batch account blade.</span></span>

![Batch account blade in Azure portal][account_blade]

* <span data-ttu-id="d85ce-189">**Batch account URL**: When you develop an application with the [Batch APIs](batch-apis-tools.md#batch-development-apis), you'll need an account URL to access your Batch resources.</span><span class="sxs-lookup"><span data-stu-id="d85ce-189">**Batch account URL**: When you develop an application with the [Batch APIs](batch-apis-tools.md#batch-development-apis), you'll need an account URL to access your Batch resources.</span></span> <span data-ttu-id="d85ce-190">A Batch account URL has the following format:</span><span class="sxs-lookup"><span data-stu-id="d85ce-190">A Batch account URL has the following format:</span></span>
  
    `https://<account_name>.<region>.batch.azure.com`

![Batch account URL in portal][account_url]

* <span data-ttu-id="d85ce-192">**Access keys** (Batch service mode): To authenticate access to your Batch account from your application, you'll need an account access key.</span><span class="sxs-lookup"><span data-stu-id="d85ce-192">**Access keys** (Batch service mode): To authenticate access to your Batch account from your application, you'll need an account access key.</span></span> <span data-ttu-id="d85ce-193">(This setting is not available in user subscription mode, where you use Azure Active Directory authetication.)</span><span class="sxs-lookup"><span data-stu-id="d85ce-193">(This setting is not available in user subscription mode, where you use Azure Active Directory authetication.)</span></span>

    <span data-ttu-id="d85ce-194">To view or regenerate your Batch account's access keys, enter `keys` in the left menu **Search** box on the Batch account blade, then select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="d85ce-194">To view or regenerate your Batch account's access keys, enter `keys` in the left menu **Search** box on the Batch account blade, then select **Keys**.</span></span> 
  
    ![Batch account keys in Azure portal][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a><span data-ttu-id="d85ce-196">Linked Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="d85ce-196">Linked Azure Storage account</span></span>

<span data-ttu-id="d85ce-197">You can optionally link a general-purpose Azure Storage account to your Batch account.</span><span class="sxs-lookup"><span data-stu-id="d85ce-197">You can optionally link a general-purpose Azure Storage account to your Batch account.</span></span> <span data-ttu-id="d85ce-198">The [application packages](batch-application-packages.md) feature of Batch uses Azure Blob storage, as does the [Batch File Conventions .NET](batch-task-output.md) library.</span><span class="sxs-lookup"><span data-stu-id="d85ce-198">The [application packages](batch-application-packages.md) feature of Batch uses Azure Blob storage, as does the [Batch File Conventions .NET](batch-task-output.md) library.</span></span> <span data-ttu-id="d85ce-199">These optional features assist you in deploying the applications that your Batch tasks run, and persisting the data they produce.</span><span class="sxs-lookup"><span data-stu-id="d85ce-199">These optional features assist you in deploying the applications that your Batch tasks run, and persisting the data they produce.</span></span>

<span data-ttu-id="d85ce-200">We recommend that you create a new Storage account exclusively for use by your Batch account.</span><span class="sxs-lookup"><span data-stu-id="d85ce-200">We recommend that you create a new Storage account exclusively for use by your Batch account.</span></span>

![Creating a "General purpose" storage account][storage_account]

> [!NOTE] 
> Azure Batch currently supports only the general-purpose Storage account type. This account type is described in step 5, [Create a storage account] (../storage/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/storage-create-storage-account.md).
>
>

> [!WARNING]
> Be careful when regenerating the access keys of a linked Storage account. Regenerate only one Storage account key and click **Sync Keys** on the linked Storage account blade. Wait five minutes to allow the keys to propagate to the compute nodes in your pools, then regenerate and synchronize the other key if necessary. If you regenerate both keys at the same time, your compute nodes will not be able to synchronize either key, and they will lose access to the Storage account.
> 
> 

<span data-ttu-id="d85ce-208">![Regenerating storage account keys][4]</span><span class="sxs-lookup"><span data-stu-id="d85ce-208">![Regenerating storage account keys][4]</span></span>

## <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="d85ce-209">Batch service quotas and limits</span><span class="sxs-lookup"><span data-stu-id="d85ce-209">Batch service quotas and limits</span></span>
<span data-ttu-id="d85ce-210">Please be aware that as with your Azure subscription and other Azure services, certain [quotas and limits](batch-quota-limit.md) apply to Batch accounts.</span><span class="sxs-lookup"><span data-stu-id="d85ce-210">Please be aware that as with your Azure subscription and other Azure services, certain [quotas and limits](batch-quota-limit.md) apply to Batch accounts.</span></span> <span data-ttu-id="d85ce-211">Current quotas for a Batch account appear in the portal in the account **Properties**.</span><span class="sxs-lookup"><span data-stu-id="d85ce-211">Current quotas for a Batch account appear in the portal in the account **Properties**.</span></span>

![Batch account quotas in Azure portal][quotas]



<span data-ttu-id="d85ce-213">Additionally, many of these quotas can be increased simply with a free product support request submitted in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d85ce-213">Additionally, many of these quotas can be increased simply with a free product support request submitted in the Azure portal.</span></span> <span data-ttu-id="d85ce-214">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for details on requesting quota increases.</span><span class="sxs-lookup"><span data-stu-id="d85ce-214">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for details on requesting quota increases.</span></span>

## <a name="other-batch-account-management-options"></a><span data-ttu-id="d85ce-215">Other Batch account management options</span><span class="sxs-lookup"><span data-stu-id="d85ce-215">Other Batch account management options</span></span>
<span data-ttu-id="d85ce-216">In addition to using the Azure portal, you can also create and manage Batch accounts with the following:</span><span class="sxs-lookup"><span data-stu-id="d85ce-216">In addition to using the Azure portal, you can also create and manage Batch accounts with the following:</span></span>

* [<span data-ttu-id="d85ce-217">Batch PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="d85ce-217">Batch PowerShell cmdlets</span></span>](batch-powershell-cmdlets-get-started.md)
* [<span data-ttu-id="d85ce-218">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d85ce-218">Azure CLI</span></span>](batch-cli-get-started.md)
* [<span data-ttu-id="d85ce-219">Batch Management .NET</span><span class="sxs-lookup"><span data-stu-id="d85ce-219">Batch Management .NET</span></span>](batch-management-dotnet.md)

## <a name="next-steps"></a><span data-ttu-id="d85ce-220">Next steps</span><span class="sxs-lookup"><span data-stu-id="d85ce-220">Next steps</span></span>
* <span data-ttu-id="d85ce-221">See the [Batch feature overview](batch-api-basics.md) to learn more about Batch service concepts and features.</span><span class="sxs-lookup"><span data-stu-id="d85ce-221">See the [Batch feature overview](batch-api-basics.md) to learn more about Batch service concepts and features.</span></span> <span data-ttu-id="d85ce-222">The article discusses the primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of the service's features that enable large-scale compute workload execution.</span><span class="sxs-lookup"><span data-stu-id="d85ce-222">The article discusses the primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of the service's features that enable large-scale compute workload execution.</span></span>
* <span data-ttu-id="d85ce-223">Learn the basics of developing a Batch-enabled application using the [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="d85ce-223">Learn the basics of developing a Batch-enabled application using the [Batch .NET client library](batch-dotnet-get-started.md) or [Python](batch-python-tutorial.md).</span></span> <span data-ttu-id="d85ce-224">These introductory articles guide you through a working application that uses the Batch service to execute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span><span class="sxs-lookup"><span data-stu-id="d85ce-224">These introductory articles guide you through a working application that uses the Batch service to execute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span></span>

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-account-create-portal/batch_acct_04.png "Regenerating storage account keys"
[marketplace_portal]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-account-create-portal/batch_blade.png
[account_portal]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-account-create-portal/account_keys.PNG
[account_url]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-account-create-portal/account_url.png
[storage_account]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-account-create-portal/storage_account.png
[quotas]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-account-create-portal/quotas.png
[subscription_access]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-account-create-portal/subscription_iam.png
[add_permission]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-account-create-portal/add_permission.png
[account_portal_byos]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-account-create-portal/batch_acct_portal_byos.png










