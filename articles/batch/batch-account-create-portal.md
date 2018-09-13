---
title: Create a Batch account in the Azure portal | Microsoft Docs
description: Learn how to create an Azure Batch account in the Azure portal to run large-scale parallel workloads in the cloud
services: batch
documentationcenter: ''
author: dlepow
manager: jeconnoc
editor: ''
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/18/2018
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dfaee72be883ee8902fe4550890d757f114ff932
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776496"
---
# <a name="create-a-batch-account-with-the-azure-portal"></a><span data-ttu-id="ff4cd-103">Create a Batch account with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ff4cd-103">Create a Batch account with the Azure portal</span></span>

<span data-ttu-id="ff4cd-104">Learn how to create an Azure Batch account in the [Azure portal][azure_portal], and choose the account properties that fit your compute scenario.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-104">Learn how to create an Azure Batch account in the [Azure portal][azure_portal], and choose the account properties that fit your compute scenario.</span></span> <span data-ttu-id="ff4cd-105">Learn where to find important account properties like access keys and account URLs.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-105">Learn where to find important account properties like access keys and account URLs.</span></span>

<span data-ttu-id="ff4cd-106">For background about Batch accounts and scenarios, see the [feature overview](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="ff4cd-106">For background about Batch accounts and scenarios, see the [feature overview](batch-api-basics.md).</span></span>

## <a name="create-a-batch-account"></a><span data-ttu-id="ff4cd-107">Create a Batch account</span><span class="sxs-lookup"><span data-stu-id="ff4cd-107">Create a Batch account</span></span>

[!INCLUDE [batch-account-mode-include](../../includes/batch-account-mode-include.md)]

1. <span data-ttu-id="ff4cd-108">Sign in to the [Azure portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="ff4cd-108">Sign in to the [Azure portal][azure_portal].</span></span>

1. <span data-ttu-id="ff4cd-109">Select **Create a resource** > **Compute** > **Batch Service**.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-109">Select **Create a resource** > **Compute** > **Batch Service**.</span></span>

    ![Batch in the Marketplace][marketplace_portal]

1. <span data-ttu-id="ff4cd-111">Enter **New Batch account** settings.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-111">Enter **New Batch account** settings.</span></span> <span data-ttu-id="ff4cd-112">See the following details.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-112">See the following details.</span></span>

    ![Create a Batch account][account_portal]

    <span data-ttu-id="ff4cd-114">a.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-114">a.</span></span> <span data-ttu-id="ff4cd-115">**Account name**: The name you choose must be unique within the Azure region where the account is created (see **Location** below).</span><span class="sxs-lookup"><span data-stu-id="ff4cd-115">**Account name**: The name you choose must be unique within the Azure region where the account is created (see **Location** below).</span></span> <span data-ttu-id="ff4cd-116">The account name can contain only lowercase characters or numbers, and must be 3-24 characters in length.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-116">The account name can contain only lowercase characters or numbers, and must be 3-24 characters in length.</span></span>

    <span data-ttu-id="ff4cd-117">b.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-117">b.</span></span> <span data-ttu-id="ff4cd-118">**Subscription**: The subscription in which to create the Batch account.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-118">**Subscription**: The subscription in which to create the Batch account.</span></span> <span data-ttu-id="ff4cd-119">If you have only one subscription, it is selected by default.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-119">If you have only one subscription, it is selected by default.</span></span>

    <span data-ttu-id="ff4cd-120">c.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-120">c.</span></span> <span data-ttu-id="ff4cd-121">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-121">**Resource group**: Select an existing resource group for your new Batch account, or optionally create a new one.</span></span>

    <span data-ttu-id="ff4cd-122">d.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-122">d.</span></span> <span data-ttu-id="ff4cd-123">**Location**: The Azure region in which to create the Batch account.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-123">**Location**: The Azure region in which to create the Batch account.</span></span> <span data-ttu-id="ff4cd-124">Only the regions supported by your subscription and resource group are displayed as options.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-124">Only the regions supported by your subscription and resource group are displayed as options.</span></span>

    <span data-ttu-id="ff4cd-125">e.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-125">e.</span></span> <span data-ttu-id="ff4cd-126">**Storage account** (optional): An Azure Storage account that you associate with your Batch account.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-126">**Storage account** (optional): An Azure Storage account that you associate with your Batch account.</span></span> <span data-ttu-id="ff4cd-127">This is recommended for most Batch accounts.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-127">This is recommended for most Batch accounts.</span></span> <span data-ttu-id="ff4cd-128">For storage account options in Batch, see the [Batch feature overview](batch-api-basics.md#azure-storage-account).</span><span class="sxs-lookup"><span data-stu-id="ff4cd-128">For storage account options in Batch, see the [Batch feature overview](batch-api-basics.md#azure-storage-account).</span></span> <span data-ttu-id="ff4cd-129">In the portal, select an existing storage account, or optionally create a new one.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-129">In the portal, select an existing storage account, or optionally create a new one.</span></span>

      ![Create a storage account][storage_account]

    <span data-ttu-id="ff4cd-131">f.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-131">f.</span></span> <span data-ttu-id="ff4cd-132">**Pool allocation mode**: For most scenarios, accept the default **Batch service**.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-132">**Pool allocation mode**: For most scenarios, accept the default **Batch service**.</span></span>

1. <span data-ttu-id="ff4cd-133">Select **Create** to create the account.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-133">Select **Create** to create the account.</span></span>



## <a name="view-batch-account-properties"></a><span data-ttu-id="ff4cd-134">View Batch account properties</span><span class="sxs-lookup"><span data-stu-id="ff4cd-134">View Batch account properties</span></span>
<span data-ttu-id="ff4cd-135">Once the account has been created, select the account to access its settings and properties.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-135">Once the account has been created, select the account to access its settings and properties.</span></span> <span data-ttu-id="ff4cd-136">You can access all account settings and properties by using the left menu.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-136">You can access all account settings and properties by using the left menu.</span></span>

![Batch account page in Azure portal][account_blade]

* <span data-ttu-id="ff4cd-138">**Batch account name, URL, and keys**: When you develop an application with the [Batch APIs](batch-apis-tools.md#azure-accounts-for-batch-development), you need an account URL and key to access your Batch resources.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-138">**Batch account name, URL, and keys**: When you develop an application with the [Batch APIs](batch-apis-tools.md#azure-accounts-for-batch-development), you need an account URL and key to access your Batch resources.</span></span> <span data-ttu-id="ff4cd-139">(Batch also supports Azure Active Directory authentication.)</span><span class="sxs-lookup"><span data-stu-id="ff4cd-139">(Batch also supports Azure Active Directory authentication.)</span></span>

    <span data-ttu-id="ff4cd-140">To view the Batch account access information, select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-140">To view the Batch account access information, select **Keys**.</span></span>

    ![Batch account keys in Azure portal][account_keys]

* <span data-ttu-id="ff4cd-142">To view the name and keys of the storage account associated with your Batch account, select **Storage account**.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-142">To view the name and keys of the storage account associated with your Batch account, select **Storage account**.</span></span>

* <span data-ttu-id="ff4cd-143">To view the resource quotas that apply to the Batch account, select  **Quotas**.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-143">To view the resource quotas that apply to the Batch account, select  **Quotas**.</span></span> <span data-ttu-id="ff4cd-144">For details, see [Batch service quotas and limits](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="ff4cd-144">For details, see [Batch service quotas and limits](batch-quota-limit.md).</span></span>


## <a name="additional-configuration-for-user-subscription-mode"></a><span data-ttu-id="ff4cd-145">Additional configuration for user subscription mode</span><span class="sxs-lookup"><span data-stu-id="ff4cd-145">Additional configuration for user subscription mode</span></span>

<span data-ttu-id="ff4cd-146">If you choose to create a Batch account in user subscription mode, perform the following additional steps before creating the account.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-146">If you choose to create a Batch account in user subscription mode, perform the following additional steps before creating the account.</span></span>

### <a name="allow-azure-batch-to-access-the-subscription-one-time-operation"></a><span data-ttu-id="ff4cd-147">Allow Azure Batch to access the subscription (one-time operation)</span><span class="sxs-lookup"><span data-stu-id="ff4cd-147">Allow Azure Batch to access the subscription (one-time operation)</span></span>
<span data-ttu-id="ff4cd-148">When creating your first Batch account in user subscription mode, you need to register your subscription with Batch.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-148">When creating your first Batch account in user subscription mode, you need to register your subscription with Batch.</span></span> <span data-ttu-id="ff4cd-149">(If you previously did this, skip to the next section.)</span><span class="sxs-lookup"><span data-stu-id="ff4cd-149">(If you previously did this, skip to the next section.)</span></span>

1. <span data-ttu-id="ff4cd-150">Sign in to the [Azure portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="ff4cd-150">Sign in to the [Azure portal][azure_portal].</span></span>

1. <span data-ttu-id="ff4cd-151">Select **All services** > **Subscriptions**, and select the subscription you want to use for the Batch account.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-151">Select **All services** > **Subscriptions**, and select the subscription you want to use for the Batch account.</span></span>

1. <span data-ttu-id="ff4cd-152">In the **Subscription** page, select **Resource providers**, and search for **Microsoft.Batch**.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-152">In the **Subscription** page, select **Resource providers**, and search for **Microsoft.Batch**.</span></span> <span data-ttu-id="ff4cd-153">Check that the **Microsoft.Batch** resource provider is registered in the subscription.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-153">Check that the **Microsoft.Batch** resource provider is registered in the subscription.</span></span> <span data-ttu-id="ff4cd-154">If it isn't registered, select the **Register** link.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-154">If it isn't registered, select the **Register** link.</span></span>

    ![Register Microsoft.Batch provider][register_provider]

1. <span data-ttu-id="ff4cd-156">In the **Subscription** page, select **Access control (IAM)** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-156">In the **Subscription** page, select **Access control (IAM)** > **Add**.</span></span>

    ![Subscription access control][subscription_access]

1. <span data-ttu-id="ff4cd-158">On the **Add permissions** page, select the **Contributor** role, search for the Batch API.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-158">On the **Add permissions** page, select the **Contributor** role, search for the Batch API.</span></span> <span data-ttu-id="ff4cd-159">Search for each of these strings until you find the API:</span><span class="sxs-lookup"><span data-stu-id="ff4cd-159">Search for each of these strings until you find the API:</span></span>
    1. <span data-ttu-id="ff4cd-160">**MicrosoftAzureBatch**.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-160">**MicrosoftAzureBatch**.</span></span>
    1. <span data-ttu-id="ff4cd-161">**Microsoft Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-161">**Microsoft Azure Batch**.</span></span> <span data-ttu-id="ff4cd-162">Newer Azure AD tenants may use this name.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-162">Newer Azure AD tenants may use this name.</span></span>
    1. <span data-ttu-id="ff4cd-163">**ddbf3205-c6bd-46ae-8127-60eb93363864** is the ID for the Batch API.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-163">**ddbf3205-c6bd-46ae-8127-60eb93363864** is the ID for the Batch API.</span></span> 

1. <span data-ttu-id="ff4cd-164">Once you find the Batch API, select it and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-164">Once you find the Batch API, select it and select **Save**.</span></span>

    ![Add Batch permissions][add_permission]

### <a name="create-a-key-vault"></a><span data-ttu-id="ff4cd-166">Create a key vault</span><span class="sxs-lookup"><span data-stu-id="ff4cd-166">Create a key vault</span></span>
<span data-ttu-id="ff4cd-167">In user subscription mode, an Azure key vault is required that belongs to the same resource group as the Batch account to be created.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-167">In user subscription mode, an Azure key vault is required that belongs to the same resource group as the Batch account to be created.</span></span> <span data-ttu-id="ff4cd-168">Make sure the resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-168">Make sure the resource group is in a region where Batch is [available](https://azure.microsoft.com/regions/services/) and which your subscription supports.</span></span>

1. <span data-ttu-id="ff4cd-169">In the [Azure portal][azure_portal], select **New** > **Security** > **Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-169">In the [Azure portal][azure_portal], select **New** > **Security** > **Key Vault**.</span></span>

1. <span data-ttu-id="ff4cd-170">In the **Create Key Vault** page, enter a name for the key vault, and create a resource group in the region you want for your Batch account.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-170">In the **Create Key Vault** page, enter a name for the key vault, and create a resource group in the region you want for your Batch account.</span></span> <span data-ttu-id="ff4cd-171">Leave the remaining settings at default values, then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-171">Leave the remaining settings at default values, then select **Create**.</span></span>

<span data-ttu-id="ff4cd-172">When creating the Batch account in user subscription mode, use the resource group for the key vault, specify **User subscription** as the pool allocation mode, and select the key vault.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-172">When creating the Batch account in user subscription mode, use the resource group for the key vault, specify **User subscription** as the pool allocation mode, and select the key vault.</span></span>

## <a name="other-batch-account-management-options"></a><span data-ttu-id="ff4cd-173">Other Batch account management options</span><span class="sxs-lookup"><span data-stu-id="ff4cd-173">Other Batch account management options</span></span>
<span data-ttu-id="ff4cd-174">In addition to using the Azure portal, you can create and manage Batch accounts with tools including the following:</span><span class="sxs-lookup"><span data-stu-id="ff4cd-174">In addition to using the Azure portal, you can create and manage Batch accounts with tools including the following:</span></span>

* [<span data-ttu-id="ff4cd-175">Batch PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="ff4cd-175">Batch PowerShell cmdlets</span></span>](batch-powershell-cmdlets-get-started.md)
* [<span data-ttu-id="ff4cd-176">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ff4cd-176">Azure CLI</span></span>](batch-cli-get-started.md)
* [<span data-ttu-id="ff4cd-177">Batch Management .NET</span><span class="sxs-lookup"><span data-stu-id="ff4cd-177">Batch Management .NET</span></span>](batch-management-dotnet.md)

## <a name="next-steps"></a><span data-ttu-id="ff4cd-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff4cd-178">Next steps</span></span>
* <span data-ttu-id="ff4cd-179">See the [Batch feature overview](batch-api-basics.md) to learn more about Batch service concepts and features.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-179">See the [Batch feature overview](batch-api-basics.md) to learn more about Batch service concepts and features.</span></span> <span data-ttu-id="ff4cd-180">The article discusses the primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of the service's features for large-scale compute workloads.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-180">The article discusses the primary Batch resources such as pools, compute nodes, jobs, and tasks, and provides an overview of the service's features for large-scale compute workloads.</span></span>
* <span data-ttu-id="ff4cd-181">Learn the basics of developing a Batch-enabled application using the [Batch .NET client library](quick-run-dotnet.md) or [Python](quick-run-python.md).</span><span class="sxs-lookup"><span data-stu-id="ff4cd-181">Learn the basics of developing a Batch-enabled application using the [Batch .NET client library](quick-run-dotnet.md) or [Python](quick-run-python.md).</span></span> <span data-ttu-id="ff4cd-182">These quickstarts guide you through a sample application that uses the Batch service to execute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span><span class="sxs-lookup"><span data-stu-id="ff4cd-182">These quickstarts guide you through a sample application that uses the Batch service to execute a workload on multiple compute nodes, and includes using Azure Storage for workload file staging and retrieval.</span></span>

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[marketplace_portal]: ./media/batch-account-create-portal/marketplace-batch.png
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch-account-portal.png
[account_keys]: ./media/batch-account-create-portal/batch-account-keys.png
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[register_provider]: ./media/batch-account-create-portal/register_provider.png

