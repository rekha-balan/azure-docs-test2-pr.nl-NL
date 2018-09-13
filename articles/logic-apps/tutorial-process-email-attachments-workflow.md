---
title: Build workflows that process emails and attachments - Azure Logic Apps | Microsoft Docs
description: This tutorial shows how to create automated workflows so you can process emails and attachments with Azure Logic Apps, Azure Storage, and Azure Functions
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
manager: jeconnoc
ms.topic: tutorial
ms.custom: mvc
ms.date: 07/20/2018
ms.reviewer: klam, LADocs
ms.openlocfilehash: d07342bac3f76472a4783c28cac0741906049bb2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869279"
---
# <a name="process-emails-and-attachments-with-azure-logic-apps"></a><span data-ttu-id="b1d2b-103">Process emails and attachments with Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="b1d2b-103">Process emails and attachments with Azure Logic Apps</span></span>

<span data-ttu-id="b1d2b-104">Azure Logic Apps helps you automate workflows and integrate data across Azure services, Microsoft services, other software-as-a-service (SaaS) apps, and on-premises systems.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-104">Azure Logic Apps helps you automate workflows and integrate data across Azure services, Microsoft services, other software-as-a-service (SaaS) apps, and on-premises systems.</span></span> <span data-ttu-id="b1d2b-105">This tutorial shows how you can build a [logic app](../logic-apps/logic-apps-overview.md) that handles incoming emails and any attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-105">This tutorial shows how you can build a [logic app](../logic-apps/logic-apps-overview.md) that handles incoming emails and any attachments.</span></span> <span data-ttu-id="b1d2b-106">This logic app processes that content, saves the content to Azure storage, and sends notifications for reviewing that content.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-106">This logic app processes that content, saves the content to Azure storage, and sends notifications for reviewing that content.</span></span> 

<span data-ttu-id="b1d2b-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b1d2b-108">Set up [Azure storage](../storage/common/storage-introduction.md) and Storage Explorer for checking saved emails and attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-108">Set up [Azure storage](../storage/common/storage-introduction.md) and Storage Explorer for checking saved emails and attachments.</span></span>
> * <span data-ttu-id="b1d2b-109">Create an [Azure function](../azure-functions/functions-overview.md) that removes HTML from emails.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-109">Create an [Azure function](../azure-functions/functions-overview.md) that removes HTML from emails.</span></span> <span data-ttu-id="b1d2b-110">This tutorial includes the code that you can use for this function.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-110">This tutorial includes the code that you can use for this function.</span></span>
> * <span data-ttu-id="b1d2b-111">Create a blank logic app.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-111">Create a blank logic app.</span></span>
> * <span data-ttu-id="b1d2b-112">Add a trigger that monitors emails for attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-112">Add a trigger that monitors emails for attachments.</span></span>
> * <span data-ttu-id="b1d2b-113">Add a condition that checks whether emails have attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-113">Add a condition that checks whether emails have attachments.</span></span>
> * <span data-ttu-id="b1d2b-114">Add an action that calls the Azure function when an email has attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-114">Add an action that calls the Azure function when an email has attachments.</span></span>
> * <span data-ttu-id="b1d2b-115">Add an action that creates storage blobs for emails and attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-115">Add an action that creates storage blobs for emails and attachments.</span></span>
> * <span data-ttu-id="b1d2b-116">Add an action that sends email notifications.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-116">Add an action that sends email notifications.</span></span>

<span data-ttu-id="b1d2b-117">When you're done, your logic app looks like this workflow at a high level:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-117">When you're done, your logic app looks like this workflow at a high level:</span></span>

![High-level finished logic app](./media/tutorial-process-email-attachments-workflow/overview.png)

<span data-ttu-id="b1d2b-119">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a> before you begin.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-119">If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a> before you begin.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b1d2b-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b1d2b-120">Prerequisites</span></span>

* <span data-ttu-id="b1d2b-121">An email account from an email provider supported by Logic Apps, such as Office 365 Outlook, Outlook.com, or Gmail.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-121">An email account from an email provider supported by Logic Apps, such as Office 365 Outlook, Outlook.com, or Gmail.</span></span> <span data-ttu-id="b1d2b-122">For other providers, [review the connectors list here](https://docs.microsoft.com/connectors/).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-122">For other providers, [review the connectors list here](https://docs.microsoft.com/connectors/).</span></span>

  <span data-ttu-id="b1d2b-123">This logic app uses an Office 365 Outlook account.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-123">This logic app uses an Office 365 Outlook account.</span></span> 
  <span data-ttu-id="b1d2b-124">If you use a different email account, the general steps stay the same, but your UI might appear slightly different.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-124">If you use a different email account, the general steps stay the same, but your UI might appear slightly different.</span></span>

* <span data-ttu-id="b1d2b-125">Download and install the <a href="https://storageexplorer.com/" target="_blank">free Microsoft Azure Storage Explorer</a>.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-125">Download and install the <a href="https://storageexplorer.com/" target="_blank">free Microsoft Azure Storage Explorer</a>.</span></span> <span data-ttu-id="b1d2b-126">This tool helps you check that your storage container is correctly set up.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-126">This tool helps you check that your storage container is correctly set up.</span></span>

## <a name="sign-in-to-azure-portal"></a><span data-ttu-id="b1d2b-127">Sign in to Azure portal</span><span class="sxs-lookup"><span data-stu-id="b1d2b-127">Sign in to Azure portal</span></span>

<span data-ttu-id="b1d2b-128">Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> with your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-128">Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> with your Azure account credentials.</span></span>

## <a name="set-up-storage-to-save-attachments"></a><span data-ttu-id="b1d2b-129">Set up storage to save attachments</span><span class="sxs-lookup"><span data-stu-id="b1d2b-129">Set up storage to save attachments</span></span>

<span data-ttu-id="b1d2b-130">You can save incoming emails and attachments as blobs in an [Azure storage container](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-130">You can save incoming emails and attachments as blobs in an [Azure storage container](../storage/common/storage-introduction.md).</span></span> 

1. <span data-ttu-id="b1d2b-131">Before you can create a storage container, [Create a storage account](../storage/common/storage-quickstart-create-account.md) with these settings:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-131">Before you can create a storage container, [Create a storage account](../storage/common/storage-quickstart-create-account.md) with these settings:</span></span>

   | <span data-ttu-id="b1d2b-132">Setting</span><span class="sxs-lookup"><span data-stu-id="b1d2b-132">Setting</span></span> | <span data-ttu-id="b1d2b-133">Value</span><span class="sxs-lookup"><span data-stu-id="b1d2b-133">Value</span></span> | <span data-ttu-id="b1d2b-134">Description</span><span class="sxs-lookup"><span data-stu-id="b1d2b-134">Description</span></span> | 
   |---------|-------|-------------| 
   | <span data-ttu-id="b1d2b-135">**Name**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-135">**Name**</span></span> | <span data-ttu-id="b1d2b-136">attachmentstorageacct</span><span class="sxs-lookup"><span data-stu-id="b1d2b-136">attachmentstorageacct</span></span> | <span data-ttu-id="b1d2b-137">The name for your storage account</span><span class="sxs-lookup"><span data-stu-id="b1d2b-137">The name for your storage account</span></span> | 
   | <span data-ttu-id="b1d2b-138">**Deployment model**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-138">**Deployment model**</span></span> | <span data-ttu-id="b1d2b-139">Resource manager</span><span class="sxs-lookup"><span data-stu-id="b1d2b-139">Resource manager</span></span> | <span data-ttu-id="b1d2b-140">The [deployment model](../azure-resource-manager/resource-manager-deployment-model.md) for managing resource deployment</span><span class="sxs-lookup"><span data-stu-id="b1d2b-140">The [deployment model](../azure-resource-manager/resource-manager-deployment-model.md) for managing resource deployment</span></span> | 
   | <span data-ttu-id="b1d2b-141">**Account kind**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-141">**Account kind**</span></span> | <span data-ttu-id="b1d2b-142">General purpose</span><span class="sxs-lookup"><span data-stu-id="b1d2b-142">General purpose</span></span> | <span data-ttu-id="b1d2b-143">The [storage account type](../storage/common/storage-introduction.md#types-of-storage-accounts)</span><span class="sxs-lookup"><span data-stu-id="b1d2b-143">The [storage account type](../storage/common/storage-introduction.md#types-of-storage-accounts)</span></span> | 
   | <span data-ttu-id="b1d2b-144">**Location**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-144">**Location**</span></span> | <span data-ttu-id="b1d2b-145">West US</span><span class="sxs-lookup"><span data-stu-id="b1d2b-145">West US</span></span> | <span data-ttu-id="b1d2b-146">The region where to store information about your storage account</span><span class="sxs-lookup"><span data-stu-id="b1d2b-146">The region where to store information about your storage account</span></span> | 
   | <span data-ttu-id="b1d2b-147">**Replication**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-147">**Replication**</span></span> | <span data-ttu-id="b1d2b-148">Locally redundant storage (LRS)</span><span class="sxs-lookup"><span data-stu-id="b1d2b-148">Locally redundant storage (LRS)</span></span> | <span data-ttu-id="b1d2b-149">This setting specifies how your data is copied, stored, managed, and synchronized.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-149">This setting specifies how your data is copied, stored, managed, and synchronized.</span></span> <span data-ttu-id="b1d2b-150">See [Replication](../storage/common/storage-introduction.md#replication).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-150">See [Replication](../storage/common/storage-introduction.md#replication).</span></span> | 
   | <span data-ttu-id="b1d2b-151">**Performance**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-151">**Performance**</span></span> | <span data-ttu-id="b1d2b-152">Standard</span><span class="sxs-lookup"><span data-stu-id="b1d2b-152">Standard</span></span> | <span data-ttu-id="b1d2b-153">This setting specifies the data types supported and media for storing data.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-153">This setting specifies the data types supported and media for storing data.</span></span> <span data-ttu-id="b1d2b-154">See [Types of storage accounts](../storage/common/storage-introduction.md#types-of-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-154">See [Types of storage accounts](../storage/common/storage-introduction.md#types-of-storage-accounts).</span></span> | 
   | <span data-ttu-id="b1d2b-155">**Secure transfer required**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-155">**Secure transfer required**</span></span> | <span data-ttu-id="b1d2b-156">Disabled</span><span class="sxs-lookup"><span data-stu-id="b1d2b-156">Disabled</span></span> | <span data-ttu-id="b1d2b-157">This setting specifies the security required for requests from connections.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-157">This setting specifies the security required for requests from connections.</span></span> <span data-ttu-id="b1d2b-158">See [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-158">See [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span></span> | 
   | <span data-ttu-id="b1d2b-159">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-159">**Subscription**</span></span> | <span data-ttu-id="b1d2b-160"><*your-Azure-subscription-name*></span><span class="sxs-lookup"><span data-stu-id="b1d2b-160"><*your-Azure-subscription-name*></span></span> | <span data-ttu-id="b1d2b-161">The name for your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="b1d2b-161">The name for your Azure subscription</span></span> | 
   | <span data-ttu-id="b1d2b-162">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-162">**Resource group**</span></span> | <span data-ttu-id="b1d2b-163">LA-Tutorial-RG</span><span class="sxs-lookup"><span data-stu-id="b1d2b-163">LA-Tutorial-RG</span></span> | <span data-ttu-id="b1d2b-164">The name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) used to organize and manage related resources.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-164">The name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) used to organize and manage related resources.</span></span> <p><span data-ttu-id="b1d2b-165">**Note:** A resource group exists inside a specific region.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-165">**Note:** A resource group exists inside a specific region.</span></span> <span data-ttu-id="b1d2b-166">Although the items in this tutorial might not be available in all regions, try to use the same region when possible.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-166">Although the items in this tutorial might not be available in all regions, try to use the same region when possible.</span></span> | 
   | <span data-ttu-id="b1d2b-167">**Configure virtual networks**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-167">**Configure virtual networks**</span></span> | <span data-ttu-id="b1d2b-168">Disabled</span><span class="sxs-lookup"><span data-stu-id="b1d2b-168">Disabled</span></span> | <span data-ttu-id="b1d2b-169">For this tutorial, keep the **Disabled** setting.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-169">For this tutorial, keep the **Disabled** setting.</span></span> | 
   |||| 

   <span data-ttu-id="b1d2b-170">To create your storage account, you can also use [Azure PowerShell](../storage/common/storage-quickstart-create-storage-account-powershell.md) or [Azure CLI](../storage/common/storage-quickstart-create-storage-account-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-170">To create your storage account, you can also use [Azure PowerShell](../storage/common/storage-quickstart-create-storage-account-powershell.md) or [Azure CLI](../storage/common/storage-quickstart-create-storage-account-cli.md).</span></span>

2. <span data-ttu-id="b1d2b-171">After Azure deploys your storage account, get your storage account's access key:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-171">After Azure deploys your storage account, get your storage account's access key:</span></span>

   1. <span data-ttu-id="b1d2b-172">On your storage account menu, under **Settings**, select **Access keys**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-172">On your storage account menu, under **Settings**, select **Access keys**.</span></span> 

   2. <span data-ttu-id="b1d2b-173">Copy your storage account name and **key1**, and then save those values somewhere safe.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-173">Copy your storage account name and **key1**, and then save those values somewhere safe.</span></span>

      ![Copy and save storage account name and key](./media/tutorial-process-email-attachments-workflow/copy-save-storage-name-key.png)

   <span data-ttu-id="b1d2b-175">To get your storage account's access key, you can also use [Azure PowerShell](https://docs.microsoft.com/powershell/module/azurerm.storage/get-azurermstorageaccountkey) or [Azure CLI](https://docs.microsoft.com/cli/azure/storage/account/keys?view=azure-cli-latest.md#az-storage-account-keys-list).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-175">To get your storage account's access key, you can also use [Azure PowerShell](https://docs.microsoft.com/powershell/module/azurerm.storage/get-azurermstorageaccountkey) or [Azure CLI](https://docs.microsoft.com/cli/azure/storage/account/keys?view=azure-cli-latest.md#az-storage-account-keys-list).</span></span> 

3. <span data-ttu-id="b1d2b-176">Create a blob storage container for your email attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-176">Create a blob storage container for your email attachments.</span></span>
   
   1. <span data-ttu-id="b1d2b-177">On your storage account menu, select **Overview**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-177">On your storage account menu, select **Overview**.</span></span> 
   <span data-ttu-id="b1d2b-178">Under **Services**, select **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-178">Under **Services**, select **Blobs**.</span></span>

      ![Add blob storage container](./media/tutorial-process-email-attachments-workflow/create-storage-container.png)

   2. <span data-ttu-id="b1d2b-180">After the **Containers** page opens, on the toolbar, select **Container**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-180">After the **Containers** page opens, on the toolbar, select **Container**.</span></span> 

   3. <span data-ttu-id="b1d2b-181">Under **New container**, enter "attachments" as your container name.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-181">Under **New container**, enter "attachments" as your container name.</span></span> 
   <span data-ttu-id="b1d2b-182">Under **Public access level**, select **Container (anonymous read access for containers and blobs)**, and then choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-182">Under **Public access level**, select **Container (anonymous read access for containers and blobs)**, and then choose **OK**.</span></span>

      <span data-ttu-id="b1d2b-183">When you're done, you can find your storage container in your storage account here in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-183">When you're done, you can find your storage container in your storage account here in the Azure portal:</span></span>

      ![Finished storage container](./media/tutorial-process-email-attachments-workflow/created-storage-container.png)

   <span data-ttu-id="b1d2b-185">To create a storage container, you can also use [Azure PowerShell](https://docs.microsoft.com/powershell/module/azure.storage/new-azurestoragecontainer), or [Azure CLI](https://docs.microsoft.com/cli/azure/storage/container?view=azure-cli-latest#az-storage-container-create).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-185">To create a storage container, you can also use [Azure PowerShell](https://docs.microsoft.com/powershell/module/azure.storage/new-azurestoragecontainer), or [Azure CLI](https://docs.microsoft.com/cli/azure/storage/container?view=azure-cli-latest#az-storage-container-create).</span></span> 

<span data-ttu-id="b1d2b-186">Next, connect Storage Explorer to your storage account.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-186">Next, connect Storage Explorer to your storage account.</span></span>

## <a name="set-up-storage-explorer"></a><span data-ttu-id="b1d2b-187">Set up Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="b1d2b-187">Set up Storage Explorer</span></span>

<span data-ttu-id="b1d2b-188">Now, connect Storage Explorer to your storage account so you can confirm that your logic app can correctly save attachments as blobs in your storage container.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-188">Now, connect Storage Explorer to your storage account so you can confirm that your logic app can correctly save attachments as blobs in your storage container.</span></span>

1. <span data-ttu-id="b1d2b-189">Open Microsoft Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-189">Open Microsoft Azure Storage Explorer.</span></span> 

   <span data-ttu-id="b1d2b-190">Storage Explorer prompts you for a connection to your storage account.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-190">Storage Explorer prompts you for a connection to your storage account.</span></span> 

2. <span data-ttu-id="b1d2b-191">In the **Connect to Azure Storage** pane, select **Use a storage account name and key**, and then choose **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-191">In the **Connect to Azure Storage** pane, select **Use a storage account name and key**, and then choose **Next**.</span></span> 

   ![Storage Explorer - Connect to storage account](./media/tutorial-process-email-attachments-workflow/storage-explorer-choose-storage-account.png)

   > [!TIP]
   > <span data-ttu-id="b1d2b-193">If no prompt appears, on the Storage Explorer toolbar, choose **Add account**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-193">If no prompt appears, on the Storage Explorer toolbar, choose **Add account**.</span></span>

3. <span data-ttu-id="b1d2b-194">Under **Account name**, provide your storage account name.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-194">Under **Account name**, provide your storage account name.</span></span> <span data-ttu-id="b1d2b-195">Under **Account key**, provide the access key you previously saved.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-195">Under **Account key**, provide the access key you previously saved.</span></span> <span data-ttu-id="b1d2b-196">Choose **Next**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-196">Choose **Next**.</span></span>

4. <span data-ttu-id="b1d2b-197">Confirm your connection information, and then choose **Connect**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-197">Confirm your connection information, and then choose **Connect**.</span></span> 

   <span data-ttu-id="b1d2b-198">Storage Explorer creates the connection, and shows your storage account in the Explorer window under **(Local and Attached)** > **Storage Accounts**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-198">Storage Explorer creates the connection, and shows your storage account in the Explorer window under **(Local and Attached)** > **Storage Accounts**.</span></span> 

5. <span data-ttu-id="b1d2b-199">To find your blob storage container, under **Storage Accounts**, expand your storage account, which is **attachmentstorageacct** here, and then expand **Blob Containers** where you find the **attachments** container, for example:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-199">To find your blob storage container, under **Storage Accounts**, expand your storage account, which is **attachmentstorageacct** here, and then expand **Blob Containers** where you find the **attachments** container, for example:</span></span> 

   ![Storage Explorer - find storage container](./media/tutorial-process-email-attachments-workflow/storage-explorer-check-contianer.png)

<span data-ttu-id="b1d2b-201">Next, create an [Azure function](../azure-functions/functions-overview.md) that removes HTML from incoming email.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-201">Next, create an [Azure function](../azure-functions/functions-overview.md) that removes HTML from incoming email.</span></span>

## <a name="create-function-to-clean-html"></a><span data-ttu-id="b1d2b-202">Create function to clean HTML</span><span class="sxs-lookup"><span data-stu-id="b1d2b-202">Create function to clean HTML</span></span>

<span data-ttu-id="b1d2b-203">Now, use the code snippet provided by these steps to create an Azure function that removes HTML from each incoming email.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-203">Now, use the code snippet provided by these steps to create an Azure function that removes HTML from each incoming email.</span></span> <span data-ttu-id="b1d2b-204">That way, the email content is cleaner and easier to process.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-204">That way, the email content is cleaner and easier to process.</span></span> <span data-ttu-id="b1d2b-205">You can then call this function from your logic app.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-205">You can then call this function from your logic app.</span></span>

1. <span data-ttu-id="b1d2b-206">Before you can create a function, [create a function app](../azure-functions/functions-create-function-app-portal.md) with these settings:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-206">Before you can create a function, [create a function app](../azure-functions/functions-create-function-app-portal.md) with these settings:</span></span>

   | <span data-ttu-id="b1d2b-207">Setting</span><span class="sxs-lookup"><span data-stu-id="b1d2b-207">Setting</span></span> | <span data-ttu-id="b1d2b-208">Value</span><span class="sxs-lookup"><span data-stu-id="b1d2b-208">Value</span></span> | <span data-ttu-id="b1d2b-209">Description</span><span class="sxs-lookup"><span data-stu-id="b1d2b-209">Description</span></span> | 
   | ------- | ----- | ----------- | 
   | <span data-ttu-id="b1d2b-210">**App name**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-210">**App name**</span></span> | <span data-ttu-id="b1d2b-211">CleanTextFunctionApp</span><span class="sxs-lookup"><span data-stu-id="b1d2b-211">CleanTextFunctionApp</span></span> | <span data-ttu-id="b1d2b-212">A globally unique and descriptive name for your function app</span><span class="sxs-lookup"><span data-stu-id="b1d2b-212">A globally unique and descriptive name for your function app</span></span> | 
   | <span data-ttu-id="b1d2b-213">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-213">**Subscription**</span></span> | <span data-ttu-id="b1d2b-214"><*your-Azure-subscription-name*></span><span class="sxs-lookup"><span data-stu-id="b1d2b-214"><*your-Azure-subscription-name*></span></span> | <span data-ttu-id="b1d2b-215">The same Azure subscription that you previously used</span><span class="sxs-lookup"><span data-stu-id="b1d2b-215">The same Azure subscription that you previously used</span></span> | 
   | <span data-ttu-id="b1d2b-216">**Resource Group**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-216">**Resource Group**</span></span> | <span data-ttu-id="b1d2b-217">LA-Tutorial-RG</span><span class="sxs-lookup"><span data-stu-id="b1d2b-217">LA-Tutorial-RG</span></span> | <span data-ttu-id="b1d2b-218">The same Azure resource group that you previously used</span><span class="sxs-lookup"><span data-stu-id="b1d2b-218">The same Azure resource group that you previously used</span></span> | 
   | <span data-ttu-id="b1d2b-219">**Hosting Plan**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-219">**Hosting Plan**</span></span> | <span data-ttu-id="b1d2b-220">Consumption Plan</span><span class="sxs-lookup"><span data-stu-id="b1d2b-220">Consumption Plan</span></span> | <span data-ttu-id="b1d2b-221">This setting determines how to allocate and scale resources, such as computing power, for running your function app.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-221">This setting determines how to allocate and scale resources, such as computing power, for running your function app.</span></span> <span data-ttu-id="b1d2b-222">See [hosting plans comparison](../azure-functions/functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-222">See [hosting plans comparison](../azure-functions/functions-scale.md).</span></span> | 
   | <span data-ttu-id="b1d2b-223">**Location**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-223">**Location**</span></span> | <span data-ttu-id="b1d2b-224">West US</span><span class="sxs-lookup"><span data-stu-id="b1d2b-224">West US</span></span> | <span data-ttu-id="b1d2b-225">The same region that you previously used</span><span class="sxs-lookup"><span data-stu-id="b1d2b-225">The same region that you previously used</span></span> | 
   | <span data-ttu-id="b1d2b-226">**Storage**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-226">**Storage**</span></span> | <span data-ttu-id="b1d2b-227">cleantextfunctionstorageacct</span><span class="sxs-lookup"><span data-stu-id="b1d2b-227">cleantextfunctionstorageacct</span></span> | <span data-ttu-id="b1d2b-228">Create a storage account for your function app.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-228">Create a storage account for your function app.</span></span> <span data-ttu-id="b1d2b-229">Use only lowercase letters and numbers.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-229">Use only lowercase letters and numbers.</span></span> <p><span data-ttu-id="b1d2b-230">**Note:** This storage account contains your function apps, and differs from your previously created storage account for email attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-230">**Note:** This storage account contains your function apps, and differs from your previously created storage account for email attachments.</span></span> | 
   | <span data-ttu-id="b1d2b-231">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-231">**Application Insights**</span></span> | <span data-ttu-id="b1d2b-232">Off</span><span class="sxs-lookup"><span data-stu-id="b1d2b-232">Off</span></span> | <span data-ttu-id="b1d2b-233">Turns on application monitoring with [Application Insights](../application-insights/app-insights-overview.md), but for this tutorial, choose the **Off** setting.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-233">Turns on application monitoring with [Application Insights](../application-insights/app-insights-overview.md), but for this tutorial, choose the **Off** setting.</span></span> | 
   |||| 

   <span data-ttu-id="b1d2b-234">If your function app doesn't automatically open after deployment, find your app in the <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-234">If your function app doesn't automatically open after deployment, find your app in the <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span> <span data-ttu-id="b1d2b-235">On the main Azure menu, select **Function Apps**, and select your function app.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-235">On the main Azure menu, select **Function Apps**, and select your function app.</span></span> 

   ![Select function app](./media/tutorial-process-email-attachments-workflow/select-function-app.png)

   <span data-ttu-id="b1d2b-237">If **Function Apps** doesn't appear on the Azure menu, go to **All services** instead.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-237">If **Function Apps** doesn't appear on the Azure menu, go to **All services** instead.</span></span> <span data-ttu-id="b1d2b-238">In the search box, find and select **Function Apps**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-238">In the search box, find and select **Function Apps**.</span></span> <span data-ttu-id="b1d2b-239">For more information, see [Create your function](../azure-functions/functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-239">For more information, see [Create your function](../azure-functions/functions-create-first-azure-function.md).</span></span>

   <span data-ttu-id="b1d2b-240">Otherwise, Azure automatically opens your function app as shown here:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-240">Otherwise, Azure automatically opens your function app as shown here:</span></span>

   ![Created function app](./media/tutorial-process-email-attachments-workflow/function-app-created.png)

   <span data-ttu-id="b1d2b-242">To create a function app, you can also use [Azure CLI](../azure-functions/functions-create-first-azure-function-azure-cli.md), or [PowerShell and Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-242">To create a function app, you can also use [Azure CLI](../azure-functions/functions-create-first-azure-function-azure-cli.md), or [PowerShell and Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

2. <span data-ttu-id="b1d2b-243">Under **Function Apps**, expand **CleanTextFunctionApp**, and select **Functions**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-243">Under **Function Apps**, expand **CleanTextFunctionApp**, and select **Functions**.</span></span> <span data-ttu-id="b1d2b-244">On the functions toolbar, select **New function**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-244">On the functions toolbar, select **New function**.</span></span>

   ![Create new function](./media/tutorial-process-email-attachments-workflow/function-app-new-function.png)

3. <span data-ttu-id="b1d2b-246">Under **Choose a template below or go to the quickstart**, open the **Scenario** list, and select **Core**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-246">Under **Choose a template below or go to the quickstart**, open the **Scenario** list, and select **Core**.</span></span> <span data-ttu-id="b1d2b-247">In the **HTTP Trigger** template, select **C#**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-247">In the **HTTP Trigger** template, select **C#**.</span></span>

   ![Select function template](./media/tutorial-process-email-attachments-workflow/function-select-httptrigger-csharp-function-template.png)

   > [!NOTE]
   > <span data-ttu-id="b1d2b-249">This example provides you the C# sample code so you can follow the example without having to know C#.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-249">This example provides you the C# sample code so you can follow the example without having to know C#.</span></span>

4. <span data-ttu-id="b1d2b-250">In the **New Function** pane, under **Name**, enter ```RemoveHTMLFunction```.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-250">In the **New Function** pane, under **Name**, enter ```RemoveHTMLFunction```.</span></span> <span data-ttu-id="b1d2b-251">Keep **Authorization level** set to **Function**, and choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-251">Keep **Authorization level** set to **Function**, and choose **Create**.</span></span>

   ![Name your function](./media/tutorial-process-email-attachments-workflow/function-provide-name.png)

5. <span data-ttu-id="b1d2b-253">After the editor opens, replace the template code with this sample code, which removes the HTML and returns results to the caller:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-253">After the editor opens, replace the template code with this sample code, which removes the HTML and returns results to the caller:</span></span>

   ``` CSharp
   using System.Net;
   using System.Text.RegularExpressions;

   public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
   {
      log.Info($"HttpWebhook triggered");

      // Parse query parameter
      string emailBodyContent = await req.Content.ReadAsStringAsync();

      // Replace HTML with other characters
      string updatedBody = Regex.Replace(emailBodyContent, "<.*?>", string.Empty);
      updatedBody = updatedBody.Replace("\\r\\n", " ");
      updatedBody = updatedBody.Replace(@"&nbsp;", " ");

      // Return cleaned text
      return req.CreateResponse(HttpStatusCode.OK, new { updatedBody });
   }
   ```

6. <span data-ttu-id="b1d2b-254">When you're done, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-254">When you're done, choose **Save**.</span></span> <span data-ttu-id="b1d2b-255">To test your function, at the editor's right edge, under the arrow (**<**) icon, choose **Test**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-255">To test your function, at the editor's right edge, under the arrow (**<**) icon, choose **Test**.</span></span> 

   ![Open the "Test" pane](./media/tutorial-process-email-attachments-workflow/function-choose-test.png)

7. <span data-ttu-id="b1d2b-257">In the **Test** pane, under **Request body**, enter this line, and choose **Run**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-257">In the **Test** pane, under **Request body**, enter this line, and choose **Run**.</span></span>

   ```json
   {"name": "<p><p>Testing my function</br></p></p>"}
   ```

   ![Test your function](./media/tutorial-process-email-attachments-workflow/function-run-test.png)

   <span data-ttu-id="b1d2b-259">The **Output** window shows the function's result:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-259">The **Output** window shows the function's result:</span></span>

   ```json
   {"updatedBody":"{\"name\": \"Testing my function\"}"}
   ```

<span data-ttu-id="b1d2b-260">After checking that your function works, create your logic app.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-260">After checking that your function works, create your logic app.</span></span> <span data-ttu-id="b1d2b-261">Although this tutorial shows how to create a function that removes HTML from emails, Logic Apps also provides an **HTML to Text** connector.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-261">Although this tutorial shows how to create a function that removes HTML from emails, Logic Apps also provides an **HTML to Text** connector.</span></span>

## <a name="create-your-logic-app"></a><span data-ttu-id="b1d2b-262">Create your logic app</span><span class="sxs-lookup"><span data-stu-id="b1d2b-262">Create your logic app</span></span>

1. <span data-ttu-id="b1d2b-263">On the main Azure menu, select **Create a resource** > 
**Integration** > **Logic App**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-263">On the main Azure menu, select **Create a resource** > 
**Integration** > **Logic App**.</span></span>

   ![Create logic app](./media/tutorial-process-email-attachments-workflow/create-logic-app.png)

2. <span data-ttu-id="b1d2b-265">Under **Create logic app**, provide this information about your logic app as shown and described.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-265">Under **Create logic app**, provide this information about your logic app as shown and described.</span></span> <span data-ttu-id="b1d2b-266">When you're done, choose **Pin to dashboard** > **Create**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-266">When you're done, choose **Pin to dashboard** > **Create**.</span></span>

   ![Provide logic app information](./media/tutorial-process-email-attachments-workflow/create-logic-app-settings.png)

   | <span data-ttu-id="b1d2b-268">Setting</span><span class="sxs-lookup"><span data-stu-id="b1d2b-268">Setting</span></span> | <span data-ttu-id="b1d2b-269">Value</span><span class="sxs-lookup"><span data-stu-id="b1d2b-269">Value</span></span> | <span data-ttu-id="b1d2b-270">Description</span><span class="sxs-lookup"><span data-stu-id="b1d2b-270">Description</span></span> | 
   | ------- | ----- | ----------- | 
   | <span data-ttu-id="b1d2b-271">**Name**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-271">**Name**</span></span> | <span data-ttu-id="b1d2b-272">LA-ProcessAttachment</span><span class="sxs-lookup"><span data-stu-id="b1d2b-272">LA-ProcessAttachment</span></span> | <span data-ttu-id="b1d2b-273">The name for your logic app</span><span class="sxs-lookup"><span data-stu-id="b1d2b-273">The name for your logic app</span></span> | 
   | <span data-ttu-id="b1d2b-274">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-274">**Subscription**</span></span> | <span data-ttu-id="b1d2b-275"><*your-Azure-subscription-name*></span><span class="sxs-lookup"><span data-stu-id="b1d2b-275"><*your-Azure-subscription-name*></span></span> | <span data-ttu-id="b1d2b-276">The same Azure subscription that you previously used</span><span class="sxs-lookup"><span data-stu-id="b1d2b-276">The same Azure subscription that you previously used</span></span> | 
   | <span data-ttu-id="b1d2b-277">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-277">**Resource group**</span></span> | <span data-ttu-id="b1d2b-278">LA-Tutorial-RG</span><span class="sxs-lookup"><span data-stu-id="b1d2b-278">LA-Tutorial-RG</span></span> | <span data-ttu-id="b1d2b-279">The same Azure resource group that you previously used</span><span class="sxs-lookup"><span data-stu-id="b1d2b-279">The same Azure resource group that you previously used</span></span> |
   | <span data-ttu-id="b1d2b-280">**Location**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-280">**Location**</span></span> | <span data-ttu-id="b1d2b-281">West US</span><span class="sxs-lookup"><span data-stu-id="b1d2b-281">West US</span></span> | <span data-ttu-id="b1d2b-282">The same region that you previously used</span><span class="sxs-lookup"><span data-stu-id="b1d2b-282">The same region that you previously used</span></span> | 
   | <span data-ttu-id="b1d2b-283">**Log Analytics**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-283">**Log Analytics**</span></span> | <span data-ttu-id="b1d2b-284">Off</span><span class="sxs-lookup"><span data-stu-id="b1d2b-284">Off</span></span> | <span data-ttu-id="b1d2b-285">For this tutorial, choose the **Off** setting.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-285">For this tutorial, choose the **Off** setting.</span></span> | 
   |||| 

3. <span data-ttu-id="b1d2b-286">After Azure deploys your app, the Logic Apps Designer opens and shows a page with an introduction video and templates for common logic app patterns.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-286">After Azure deploys your app, the Logic Apps Designer opens and shows a page with an introduction video and templates for common logic app patterns.</span></span> <span data-ttu-id="b1d2b-287">Under **Templates**, choose **Blank Logic App**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-287">Under **Templates**, choose **Blank Logic App**.</span></span>

   ![Choose blank logic app template](./media/tutorial-process-email-attachments-workflow/choose-logic-app-template.png)

<span data-ttu-id="b1d2b-289">Next, add a [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts) that listens for incoming emails that have attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-289">Next, add a [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts) that listens for incoming emails that have attachments.</span></span> <span data-ttu-id="b1d2b-290">Every logic app must start with a trigger, which fires when a specific event happens or when new data meets a specific condition.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-290">Every logic app must start with a trigger, which fires when a specific event happens or when new data meets a specific condition.</span></span> <span data-ttu-id="b1d2b-291">For more information, see [Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-291">For more information, see [Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span>

## <a name="monitor-incoming-email"></a><span data-ttu-id="b1d2b-292">Monitor incoming email</span><span class="sxs-lookup"><span data-stu-id="b1d2b-292">Monitor incoming email</span></span>

1. <span data-ttu-id="b1d2b-293">On the designer in the search box, enter "when new email arrives" as your filter.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-293">On the designer in the search box, enter "when new email arrives" as your filter.</span></span> <span data-ttu-id="b1d2b-294">Select this trigger for your email provider: **When a new email arrives - <*your-email-provider*>**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-294">Select this trigger for your email provider: **When a new email arrives - <*your-email-provider*>**</span></span>

   <span data-ttu-id="b1d2b-295">For example:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-295">For example:</span></span>

   ![Select this trigger for email provider: "When a new email arrives"](./media/tutorial-process-email-attachments-workflow/add-trigger-when-email-arrives.png)

   * <span data-ttu-id="b1d2b-297">For Azure work or school accounts, select Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-297">For Azure work or school accounts, select Office 365 Outlook.</span></span> 
   * <span data-ttu-id="b1d2b-298">For personal Microsoft accounts, select Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-298">For personal Microsoft accounts, select Outlook.com.</span></span> 

2. <span data-ttu-id="b1d2b-299">If you're asked for credentials, sign in to your email account so Logic Apps can connect to your email account.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-299">If you're asked for credentials, sign in to your email account so Logic Apps can connect to your email account.</span></span>

3. <span data-ttu-id="b1d2b-300">Now provide the criteria the trigger uses to filter new email.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-300">Now provide the criteria the trigger uses to filter new email.</span></span>

   1. <span data-ttu-id="b1d2b-301">Specify the folder, interval, and frequency for checking emails.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-301">Specify the folder, interval, and frequency for checking emails.</span></span>

      ![Specify folder, interval, and frequency for checking mails](./media/tutorial-process-email-attachments-workflow/set-up-email-trigger.png)

      | <span data-ttu-id="b1d2b-303">Setting</span><span class="sxs-lookup"><span data-stu-id="b1d2b-303">Setting</span></span> | <span data-ttu-id="b1d2b-304">Value</span><span class="sxs-lookup"><span data-stu-id="b1d2b-304">Value</span></span> | <span data-ttu-id="b1d2b-305">Description</span><span class="sxs-lookup"><span data-stu-id="b1d2b-305">Description</span></span> | 
      | ------- | ----- | ----------- | 
      | <span data-ttu-id="b1d2b-306">**Folder**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-306">**Folder**</span></span> | <span data-ttu-id="b1d2b-307">Inbox</span><span class="sxs-lookup"><span data-stu-id="b1d2b-307">Inbox</span></span> | <span data-ttu-id="b1d2b-308">The email folder to check</span><span class="sxs-lookup"><span data-stu-id="b1d2b-308">The email folder to check</span></span> | 
      | <span data-ttu-id="b1d2b-309">**Interval**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-309">**Interval**</span></span> | <span data-ttu-id="b1d2b-310">1</span><span class="sxs-lookup"><span data-stu-id="b1d2b-310">1</span></span> | <span data-ttu-id="b1d2b-311">The number of intervals to wait between checks</span><span class="sxs-lookup"><span data-stu-id="b1d2b-311">The number of intervals to wait between checks</span></span> | 
      | <span data-ttu-id="b1d2b-312">**Frequency**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-312">**Frequency**</span></span> | <span data-ttu-id="b1d2b-313">Minute</span><span class="sxs-lookup"><span data-stu-id="b1d2b-313">Minute</span></span> | <span data-ttu-id="b1d2b-314">The unit of time for each interval between checks</span><span class="sxs-lookup"><span data-stu-id="b1d2b-314">The unit of time for each interval between checks</span></span> | 
      |  |  |  | 
  
   2. <span data-ttu-id="b1d2b-315">Choose **Show advanced options** and specify these settings:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-315">Choose **Show advanced options** and specify these settings:</span></span>

      | <span data-ttu-id="b1d2b-316">Setting</span><span class="sxs-lookup"><span data-stu-id="b1d2b-316">Setting</span></span> | <span data-ttu-id="b1d2b-317">Value</span><span class="sxs-lookup"><span data-stu-id="b1d2b-317">Value</span></span> | <span data-ttu-id="b1d2b-318">Description</span><span class="sxs-lookup"><span data-stu-id="b1d2b-318">Description</span></span> | 
      | ------- | ----- | ----------- | 
      | <span data-ttu-id="b1d2b-319">**Has Attachment**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-319">**Has Attachment**</span></span> | <span data-ttu-id="b1d2b-320">Yes</span><span class="sxs-lookup"><span data-stu-id="b1d2b-320">Yes</span></span> | <span data-ttu-id="b1d2b-321">Get only emails with attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-321">Get only emails with attachments.</span></span> <p><span data-ttu-id="b1d2b-322">**Note:** The trigger doesn't remove any emails from your account, checking only new messages and processing only emails that match the subject filter.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-322">**Note:** The trigger doesn't remove any emails from your account, checking only new messages and processing only emails that match the subject filter.</span></span> | 
      | <span data-ttu-id="b1d2b-323">**Include Attachments**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-323">**Include Attachments**</span></span> | <span data-ttu-id="b1d2b-324">Yes</span><span class="sxs-lookup"><span data-stu-id="b1d2b-324">Yes</span></span> | <span data-ttu-id="b1d2b-325">Get the attachments as input for your workflow, rather than just check for attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-325">Get the attachments as input for your workflow, rather than just check for attachments.</span></span> | 
      | <span data-ttu-id="b1d2b-326">**Subject Filter**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-326">**Subject Filter**</span></span> | ```Business Analyst 2 #423501``` | <span data-ttu-id="b1d2b-327">The text to find in the email subject</span><span class="sxs-lookup"><span data-stu-id="b1d2b-327">The text to find in the email subject</span></span> | 
      |  |  |  | 

4. <span data-ttu-id="b1d2b-328">To hide the trigger's details for now, click inside the trigger's title bar.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-328">To hide the trigger's details for now, click inside the trigger's title bar.</span></span>

   ![Collapse shape to hide details](./media/tutorial-process-email-attachments-workflow/collapse-trigger-shape.png)

5. <span data-ttu-id="b1d2b-330">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-330">Save your logic app.</span></span> <span data-ttu-id="b1d2b-331">On the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-331">On the designer toolbar, choose **Save**.</span></span>

   <span data-ttu-id="b1d2b-332">Your logic app is now live but doesn't do anything other check your emails.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-332">Your logic app is now live but doesn't do anything other check your emails.</span></span> 
   <span data-ttu-id="b1d2b-333">Next, add a condition that specifies criteria to continue workflow.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-333">Next, add a condition that specifies criteria to continue workflow.</span></span>

## <a name="check-for-attachments"></a><span data-ttu-id="b1d2b-334">Check for attachments</span><span class="sxs-lookup"><span data-stu-id="b1d2b-334">Check for attachments</span></span>

<span data-ttu-id="b1d2b-335">Now add a condition that selects only emails that have attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-335">Now add a condition that selects only emails that have attachments.</span></span>

1. <span data-ttu-id="b1d2b-336">Under the trigger, choose **New step** > **Add a condition**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-336">Under the trigger, choose **New step** > **Add a condition**.</span></span>

   !["New step", "Add a condition"](./media/tutorial-process-email-attachments-workflow/add-condition-under-trigger.png)

2. <span data-ttu-id="b1d2b-338">Rename the condition with a better description.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-338">Rename the condition with a better description.</span></span>

   1. <span data-ttu-id="b1d2b-339">On the condition's title bar, choose **ellipses** (**...**) button > **Rename**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-339">On the condition's title bar, choose **ellipses** (**...**) button > **Rename**.</span></span>

      ![Rename condition](./media/tutorial-process-email-attachments-workflow/condition-rename.png)

   2. <span data-ttu-id="b1d2b-341">Rename your condition with this description: ```If email has attachments and key subject phrase```</span><span class="sxs-lookup"><span data-stu-id="b1d2b-341">Rename your condition with this description: ```If email has attachments and key subject phrase```</span></span>

3. <span data-ttu-id="b1d2b-342">Create a condition that checks for emails that have attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-342">Create a condition that checks for emails that have attachments.</span></span> 

   1. <span data-ttu-id="b1d2b-343">On the first row under **And**, click inside the left box.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-343">On the first row under **And**, click inside the left box.</span></span> 
   <span data-ttu-id="b1d2b-344">From the dynamic content list that appears, select the **Has Attachment** property.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-344">From the dynamic content list that appears, select the **Has Attachment** property.</span></span>

      ![Build condition](./media/tutorial-process-email-attachments-workflow/build-condition.png)

   2. <span data-ttu-id="b1d2b-346">In the middle box, keep the operator **is equal to**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-346">In the middle box, keep the operator **is equal to**.</span></span>

   3. <span data-ttu-id="b1d2b-347">In the right box, enter **True** as the value to compare with the **Has Attachment** property value from the trigger.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-347">In the right box, enter **True** as the value to compare with the **Has Attachment** property value from the trigger.</span></span>

      ![Build condition](./media/tutorial-process-email-attachments-workflow/finished-condition.png)

      <span data-ttu-id="b1d2b-349">If both values are equal, the email has at least one attachment, the condition passes, and the workflow continues.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-349">If both values are equal, the email has at least one attachment, the condition passes, and the workflow continues.</span></span>

   <span data-ttu-id="b1d2b-350">In your underlying logic app definition, which you can view in the code editor window, this condition looks like this example:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-350">In your underlying logic app definition, which you can view in the code editor window, this condition looks like this example:</span></span>

   ```json
   "Condition": {
      "actions": { <actions-to-run-when-condition-passes> },
      "expression": {
         "and": [ {
            "equals": [
               "@triggerBody()?['HasAttachment']",
                 "True"
            ]
         } ]
      },
      "runAfter": {},
      "type": "If"
   }
   ```

4. <span data-ttu-id="b1d2b-351">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-351">Save your logic app.</span></span> <span data-ttu-id="b1d2b-352">On the designer toolbar, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-352">On the designer toolbar, choose **Save**.</span></span>

### <a name="test-your-condition"></a><span data-ttu-id="b1d2b-353">Test your condition</span><span class="sxs-lookup"><span data-stu-id="b1d2b-353">Test your condition</span></span>

<span data-ttu-id="b1d2b-354">Now, test whether the condition works correctly:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-354">Now, test whether the condition works correctly:</span></span>

1. <span data-ttu-id="b1d2b-355">If your logic app isn't running already, choose **Run** on the designer toolbar.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-355">If your logic app isn't running already, choose **Run** on the designer toolbar.</span></span>

   <span data-ttu-id="b1d2b-356">This step manually starts your logic app without having to wait until your specified interval passes.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-356">This step manually starts your logic app without having to wait until your specified interval passes.</span></span> 
   <span data-ttu-id="b1d2b-357">However, nothing happens until the test email arrives in your inbox.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-357">However, nothing happens until the test email arrives in your inbox.</span></span> 

2. <span data-ttu-id="b1d2b-358">Send yourself an email that meets this criteria:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-358">Send yourself an email that meets this criteria:</span></span>

   * <span data-ttu-id="b1d2b-359">Your email's subject has the text that you specified in the trigger's **Subject filter**: ```Business Analyst 2 #423501```</span><span class="sxs-lookup"><span data-stu-id="b1d2b-359">Your email's subject has the text that you specified in the trigger's **Subject filter**: ```Business Analyst 2 #423501```</span></span>

   * <span data-ttu-id="b1d2b-360">Your email has one attachment.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-360">Your email has one attachment.</span></span> 
   <span data-ttu-id="b1d2b-361">For now, just create one empty text file and attach that file to your email.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-361">For now, just create one empty text file and attach that file to your email.</span></span>

   <span data-ttu-id="b1d2b-362">When the email arrives, your logic app checks for attachments and the specified subject text.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-362">When the email arrives, your logic app checks for attachments and the specified subject text.</span></span>
   <span data-ttu-id="b1d2b-363">If the condition passes, the trigger fires and causes the Logic Apps engine to create a logic app instance and start the workflow.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-363">If the condition passes, the trigger fires and causes the Logic Apps engine to create a logic app instance and start the workflow.</span></span> 

3. <span data-ttu-id="b1d2b-364">To check that the trigger fired and the logic app ran successfully, on the logic app menu, choose **Overview**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-364">To check that the trigger fired and the logic app ran successfully, on the logic app menu, choose **Overview**.</span></span>

   ![Check trigger and runs history](./media/tutorial-process-email-attachments-workflow/checkpoint-run-history.png)

   <span data-ttu-id="b1d2b-366">If your logic app didn't trigger or run despite a successful trigger, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-366">If your logic app didn't trigger or run despite a successful trigger, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

<span data-ttu-id="b1d2b-367">Next, define the actions to take for the **If true** branch.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-367">Next, define the actions to take for the **If true** branch.</span></span> <span data-ttu-id="b1d2b-368">To save the email along with any attachments, remove any HTML from the email body, then create blobs in the storage container for the email and attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-368">To save the email along with any attachments, remove any HTML from the email body, then create blobs in the storage container for the email and attachments.</span></span>

> [!NOTE]
> <span data-ttu-id="b1d2b-369">Your logic app doesn't have to do anything for the **If false** branch when an email doesn't have attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-369">Your logic app doesn't have to do anything for the **If false** branch when an email doesn't have attachments.</span></span> <span data-ttu-id="b1d2b-370">As a bonus exercise after you finish this tutorial, you can add any appropriate action that you want to take for the **If false** branch.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-370">As a bonus exercise after you finish this tutorial, you can add any appropriate action that you want to take for the **If false** branch.</span></span>

## <a name="call-removehtmlfunction"></a><span data-ttu-id="b1d2b-371">Call RemoveHTMLFunction</span><span class="sxs-lookup"><span data-stu-id="b1d2b-371">Call RemoveHTMLFunction</span></span>

<span data-ttu-id="b1d2b-372">This step adds your previously created Azure function to your logic app and passes the email body content from email trigger to your function.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-372">This step adds your previously created Azure function to your logic app and passes the email body content from email trigger to your function.</span></span>

1. <span data-ttu-id="b1d2b-373">On the logic app menu, select **Logic App Designer**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-373">On the logic app menu, select **Logic App Designer**.</span></span> <span data-ttu-id="b1d2b-374">In the **If true** branch, choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-374">In the **If true** branch, choose **Add an action**.</span></span>

   ![Inside "If true", add action](./media/tutorial-process-email-attachments-workflow/if-true-add-action.png)

2. <span data-ttu-id="b1d2b-376">In the search box, find "azure functions", and select this action: **Choose an Azure function - Azure Functions**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-376">In the search box, find "azure functions", and select this action: **Choose an Azure function - Azure Functions**</span></span>

   ![Select action for "Choose an Azure function"](./media/tutorial-process-email-attachments-workflow/add-action-azure-function.png)

3. <span data-ttu-id="b1d2b-378">Select your previously created function app: **CleanTextFunctionApp**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-378">Select your previously created function app: **CleanTextFunctionApp**</span></span>

   ![Select your Azure function app](./media/tutorial-process-email-attachments-workflow/add-action-select-azure-function-app.png)

4. <span data-ttu-id="b1d2b-380">Now select your function: **RemoveHTMLFunction**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-380">Now select your function: **RemoveHTMLFunction**</span></span>

   ![Select your Azure function](./media/tutorial-process-email-attachments-workflow/add-action-select-azure-function.png)

5. <span data-ttu-id="b1d2b-382">Rename your function shape with this description: ```Call RemoveHTMLFunction to clean email body```</span><span class="sxs-lookup"><span data-stu-id="b1d2b-382">Rename your function shape with this description: ```Call RemoveHTMLFunction to clean email body```</span></span>

6. <span data-ttu-id="b1d2b-383">Now specify the input for your function to process.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-383">Now specify the input for your function to process.</span></span> 

   1. <span data-ttu-id="b1d2b-384">Under **Request Body**, enter this text with a trailing space:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-384">Under **Request Body**, enter this text with a trailing space:</span></span> 
   
      ```{ "emailBody": ``` 

      <span data-ttu-id="b1d2b-385">While you work on this input in the next steps, an error about invalid JSON appears until your input is correctly formatted as JSON.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-385">While you work on this input in the next steps, an error about invalid JSON appears until your input is correctly formatted as JSON.</span></span>
      <span data-ttu-id="b1d2b-386">When you previously tested this function, the input specified for this function used JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-386">When you previously tested this function, the input specified for this function used JavaScript Object Notation (JSON).</span></span> 
      <span data-ttu-id="b1d2b-387">So, the request body must also use the same format.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-387">So, the request body must also use the same format.</span></span>

      <span data-ttu-id="b1d2b-388">Also, when your cursor is inside the **Request body** box, the dynamic content list appears so you can select property values available from previous actions.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-388">Also, when your cursor is inside the **Request body** box, the dynamic content list appears so you can select property values available from previous actions.</span></span> 
      
   2. <span data-ttu-id="b1d2b-389">From the dynamic content list, under **When a new email arrives**, select the **Body** property.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-389">From the dynamic content list, under **When a new email arrives**, select the **Body** property.</span></span> <span data-ttu-id="b1d2b-390">After this property, remember to add the closing curly brace: ```}```</span><span class="sxs-lookup"><span data-stu-id="b1d2b-390">After this property, remember to add the closing curly brace: ```}```</span></span>

      ![Specify the request body for passing to the function](./media/tutorial-process-email-attachments-workflow/add-email-body-for-function-processing.png)

   <span data-ttu-id="b1d2b-392">When you're done, the input to your function looks like this example:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-392">When you're done, the input to your function looks like this example:</span></span>

   ![Finished request body to pass to your function](./media/tutorial-process-email-attachments-workflow/add-email-body-for-function-processing-2.png)

7. <span data-ttu-id="b1d2b-394">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-394">Save your logic app.</span></span>

<span data-ttu-id="b1d2b-395">Next, add an action that creates a blob in your storage container so you can save the email body.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-395">Next, add an action that creates a blob in your storage container so you can save the email body.</span></span>

## <a name="create-blob-for-email-body"></a><span data-ttu-id="b1d2b-396">Create blob for email body</span><span class="sxs-lookup"><span data-stu-id="b1d2b-396">Create blob for email body</span></span>

1. <span data-ttu-id="b1d2b-397">In the **If true** block and under your Azure function, choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-397">In the **If true** block and under your Azure function, choose **Add an action**.</span></span> 

2. <span data-ttu-id="b1d2b-398">In the search box, enter "create blob" as your filter, and select this action: **Create blob - Azure Blob Storage**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-398">In the search box, enter "create blob" as your filter, and select this action: **Create blob - Azure Blob Storage**</span></span>

   ![Add action to create blob for email body](./media/tutorial-process-email-attachments-workflow/create-blob-action-for-email-body.png)

3. <span data-ttu-id="b1d2b-400">Create a connection to your storage account with these settings as shown and described here.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-400">Create a connection to your storage account with these settings as shown and described here.</span></span> <span data-ttu-id="b1d2b-401">When you're done, choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-401">When you're done, choose **Create**.</span></span>

   ![Create connection to storage account](./media/tutorial-process-email-attachments-workflow/create-storage-account-connection-first.png)

   | <span data-ttu-id="b1d2b-403">Setting</span><span class="sxs-lookup"><span data-stu-id="b1d2b-403">Setting</span></span> | <span data-ttu-id="b1d2b-404">Value</span><span class="sxs-lookup"><span data-stu-id="b1d2b-404">Value</span></span> | <span data-ttu-id="b1d2b-405">Description</span><span class="sxs-lookup"><span data-stu-id="b1d2b-405">Description</span></span> | 
   | ------- | ----- | ----------- | 
   | <span data-ttu-id="b1d2b-406">**Connection Name**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-406">**Connection Name**</span></span> | <span data-ttu-id="b1d2b-407">AttachmentStorageConnection</span><span class="sxs-lookup"><span data-stu-id="b1d2b-407">AttachmentStorageConnection</span></span> | <span data-ttu-id="b1d2b-408">A descriptive name for the connection</span><span class="sxs-lookup"><span data-stu-id="b1d2b-408">A descriptive name for the connection</span></span> | 
   | <span data-ttu-id="b1d2b-409">**Storage Account**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-409">**Storage Account**</span></span> | <span data-ttu-id="b1d2b-410">attachmentstorageacct</span><span class="sxs-lookup"><span data-stu-id="b1d2b-410">attachmentstorageacct</span></span> | <span data-ttu-id="b1d2b-411">The name for the storage account that you previously created for saving attachments</span><span class="sxs-lookup"><span data-stu-id="b1d2b-411">The name for the storage account that you previously created for saving attachments</span></span> | 
   |||| 

4. <span data-ttu-id="b1d2b-412">Rename the **Create blob** action with this description: ```Create blob for email body```</span><span class="sxs-lookup"><span data-stu-id="b1d2b-412">Rename the **Create blob** action with this description: ```Create blob for email body```</span></span>

5. <span data-ttu-id="b1d2b-413">In the **Create blob** action, provide this information, and select these fields to create the blob as shown and described:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-413">In the **Create blob** action, provide this information, and select these fields to create the blob as shown and described:</span></span>

   ![Provide blob information for email body](./media/tutorial-process-email-attachments-workflow/create-blob-for-email-body.png)

   | <span data-ttu-id="b1d2b-415">Setting</span><span class="sxs-lookup"><span data-stu-id="b1d2b-415">Setting</span></span> | <span data-ttu-id="b1d2b-416">Value</span><span class="sxs-lookup"><span data-stu-id="b1d2b-416">Value</span></span> | <span data-ttu-id="b1d2b-417">Description</span><span class="sxs-lookup"><span data-stu-id="b1d2b-417">Description</span></span> | 
   | ------- | ----- | ----------- | 
   | <span data-ttu-id="b1d2b-418">**Folder path**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-418">**Folder path**</span></span> | <span data-ttu-id="b1d2b-419">/attachments</span><span class="sxs-lookup"><span data-stu-id="b1d2b-419">/attachments</span></span> | <span data-ttu-id="b1d2b-420">The path and name for the container that you previously created.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-420">The path and name for the container that you previously created.</span></span> <span data-ttu-id="b1d2b-421">For this example, click the folder icon, and then select the "/attachments" container.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-421">For this example, click the folder icon, and then select the "/attachments" container.</span></span> | 
   | <span data-ttu-id="b1d2b-422">**Blob name**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-422">**Blob name**</span></span> | <span data-ttu-id="b1d2b-423">**From** field</span><span class="sxs-lookup"><span data-stu-id="b1d2b-423">**From** field</span></span> | <span data-ttu-id="b1d2b-424">For this example, use the sender's name as the blob's name.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-424">For this example, use the sender's name as the blob's name.</span></span> <span data-ttu-id="b1d2b-425">Click inside this box so that the dynamic content list appears, and then select the **From** field under the **When a new email arrives** action.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-425">Click inside this box so that the dynamic content list appears, and then select the **From** field under the **When a new email arrives** action.</span></span> | 
   | <span data-ttu-id="b1d2b-426">**Blob content**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-426">**Blob content**</span></span> | <span data-ttu-id="b1d2b-427">**Content** field</span><span class="sxs-lookup"><span data-stu-id="b1d2b-427">**Content** field</span></span> | <span data-ttu-id="b1d2b-428">For this example, use the HTML-free email body as the blob content.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-428">For this example, use the HTML-free email body as the blob content.</span></span> <span data-ttu-id="b1d2b-429">Click inside this box so that the dynamic content list appears, and then select **Body** under the **Call RemoveHTMLFunction to clean email body** action.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-429">Click inside this box so that the dynamic content list appears, and then select **Body** under the **Call RemoveHTMLFunction to clean email body** action.</span></span> |
   |||| 

   <span data-ttu-id="b1d2b-430">When you're done, the action looks like this example:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-430">When you're done, the action looks like this example:</span></span>

   ![Finished "Create blob" action](./media/tutorial-process-email-attachments-workflow/create-blob-for-email-body-done.png)

6. <span data-ttu-id="b1d2b-432">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-432">Save your logic app.</span></span> 

### <a name="check-attachment-handling"></a><span data-ttu-id="b1d2b-433">Check attachment handling</span><span class="sxs-lookup"><span data-stu-id="b1d2b-433">Check attachment handling</span></span>

<span data-ttu-id="b1d2b-434">Now test whether your logic app handles emails the way that you specified:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-434">Now test whether your logic app handles emails the way that you specified:</span></span>

1. <span data-ttu-id="b1d2b-435">If your logic app isn't running already, choose **Run** on the designer toolbar.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-435">If your logic app isn't running already, choose **Run** on the designer toolbar.</span></span>

2. <span data-ttu-id="b1d2b-436">Send yourself an email that meets this criteria:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-436">Send yourself an email that meets this criteria:</span></span>

   * <span data-ttu-id="b1d2b-437">Your email's subject has the text that you specified in the trigger's **Subject filter**: ```Business Analyst 2 #423501```</span><span class="sxs-lookup"><span data-stu-id="b1d2b-437">Your email's subject has the text that you specified in the trigger's **Subject filter**: ```Business Analyst 2 #423501```</span></span>

   * <span data-ttu-id="b1d2b-438">Your email has at least one attachment.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-438">Your email has at least one attachment.</span></span> 
   <span data-ttu-id="b1d2b-439">For now, just create one empty text file and attach that file to your email.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-439">For now, just create one empty text file and attach that file to your email.</span></span>

   * <span data-ttu-id="b1d2b-440">Your email has some test content in the body, for example:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-440">Your email has some test content in the body, for example:</span></span> 

     ```
     Testing my logic app
     ```

   <span data-ttu-id="b1d2b-441">If your logic app didn't trigger or run despite a successful trigger, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-441">If your logic app didn't trigger or run despite a successful trigger, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

3. <span data-ttu-id="b1d2b-442">Check that your logic app saved the email to the correct storage container.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-442">Check that your logic app saved the email to the correct storage container.</span></span> 

   1. <span data-ttu-id="b1d2b-443">In Storage Explorer, expand **(Local and Attached)** > 
   **Storage Accounts** > **attachmentstorageacct (External)** > 
   **Blob Containers** > **attachments**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-443">In Storage Explorer, expand **(Local and Attached)** > 
**Storage Accounts** > **attachmentstorageacct (External)** > 
**Blob Containers** > **attachments**.</span></span>

   2. <span data-ttu-id="b1d2b-444">Check the **attachments** container for the email.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-444">Check the **attachments** container for the email.</span></span> 

      <span data-ttu-id="b1d2b-445">At this point, only the email appears in the container because the logic app doesn't process the attachments yet.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-445">At this point, only the email appears in the container because the logic app doesn't process the attachments yet.</span></span>

      ![Check Storage Explorer for saved email](./media/tutorial-process-email-attachments-workflow/storage-explorer-saved-email.png)

   3. <span data-ttu-id="b1d2b-447">When you're done, delete the email in Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-447">When you're done, delete the email in Storage Explorer.</span></span>

4. <span data-ttu-id="b1d2b-448">Optionally, to test the **If false** branch, which does nothing at this time, you can send an email that doesn't meet the criteria.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-448">Optionally, to test the **If false** branch, which does nothing at this time, you can send an email that doesn't meet the criteria.</span></span>

<span data-ttu-id="b1d2b-449">Next, add a loop to process all the email attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-449">Next, add a loop to process all the email attachments.</span></span>

## <a name="process-attachments"></a><span data-ttu-id="b1d2b-450">Process attachments</span><span class="sxs-lookup"><span data-stu-id="b1d2b-450">Process attachments</span></span>

<span data-ttu-id="b1d2b-451">To process each attachment in the email, add a **For each** loop to your logic app's workflow.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-451">To process each attachment in the email, add a **For each** loop to your logic app's workflow.</span></span>

1. <span data-ttu-id="b1d2b-452">Under the **Create blob for email body** shape, select **More** > **Add a for each**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-452">Under the **Create blob for email body** shape, select **More** > **Add a for each**.</span></span>

   ![Add "for each" loop](./media/tutorial-process-email-attachments-workflow/add-for-each-loop.png)

2. <span data-ttu-id="b1d2b-454">Rename your loop with this description: ```For each email attachment```</span><span class="sxs-lookup"><span data-stu-id="b1d2b-454">Rename your loop with this description: ```For each email attachment```</span></span>

3. <span data-ttu-id="b1d2b-455">Now specify the data for the loop to process.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-455">Now specify the data for the loop to process.</span></span> <span data-ttu-id="b1d2b-456">Click inside the **Select an output from previous steps** box so that the dynamic content list opens, and then select **Attachments**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-456">Click inside the **Select an output from previous steps** box so that the dynamic content list opens, and then select **Attachments**.</span></span> 

   ![Select "Attachments"](./media/tutorial-process-email-attachments-workflow/select-attachments.png)

   <span data-ttu-id="b1d2b-458">The **Attachments** field passes in an array that contains all the attachments included with an email.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-458">The **Attachments** field passes in an array that contains all the attachments included with an email.</span></span> 
   <span data-ttu-id="b1d2b-459">The **For each** loop repeats actions on each item that's passed in with the array.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-459">The **For each** loop repeats actions on each item that's passed in with the array.</span></span>

4. <span data-ttu-id="b1d2b-460">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-460">Save your logic app.</span></span>

<span data-ttu-id="b1d2b-461">Next, add the action that saves each attachment as a blob in your **attachments** storage container.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-461">Next, add the action that saves each attachment as a blob in your **attachments** storage container.</span></span>

## <a name="create-blob-for-each-attachment"></a><span data-ttu-id="b1d2b-462">Create blob for each attachment</span><span class="sxs-lookup"><span data-stu-id="b1d2b-462">Create blob for each attachment</span></span>

1. <span data-ttu-id="b1d2b-463">In the **For each email attachment** loop, choose **Add an action** so you can specify the task to perform on each found attachment.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-463">In the **For each email attachment** loop, choose **Add an action** so you can specify the task to perform on each found attachment.</span></span>

   ![Add action to loop](./media/tutorial-process-email-attachments-workflow/for-each-add-action.png)

2. <span data-ttu-id="b1d2b-465">In the search box, enter "create blob" as your filter, and then select this action: **Create blob - Azure Blob Storage**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-465">In the search box, enter "create blob" as your filter, and then select this action: **Create blob - Azure Blob Storage**</span></span>

   ![Add action to create blob](./media/tutorial-process-email-attachments-workflow/create-blob-action-for-attachments.png)

3. <span data-ttu-id="b1d2b-467">Rename the **Create blob 2** action with this description: ```Create blob for each email attachment```</span><span class="sxs-lookup"><span data-stu-id="b1d2b-467">Rename the **Create blob 2** action with this description: ```Create blob for each email attachment```</span></span>

4. <span data-ttu-id="b1d2b-468">In the **Create blob for each email attachment** action, provide this information, and select the properties for each blob you want to create as shown and described:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-468">In the **Create blob for each email attachment** action, provide this information, and select the properties for each blob you want to create as shown and described:</span></span>

   ![Provide blob information](./media/tutorial-process-email-attachments-workflow/create-blob-per-attachment.png)

   | <span data-ttu-id="b1d2b-470">Setting</span><span class="sxs-lookup"><span data-stu-id="b1d2b-470">Setting</span></span> | <span data-ttu-id="b1d2b-471">Value</span><span class="sxs-lookup"><span data-stu-id="b1d2b-471">Value</span></span> | <span data-ttu-id="b1d2b-472">Description</span><span class="sxs-lookup"><span data-stu-id="b1d2b-472">Description</span></span> | 
   | ------- | ----- | ----------- | 
   | <span data-ttu-id="b1d2b-473">**Folder path**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-473">**Folder path**</span></span> | <span data-ttu-id="b1d2b-474">/attachments</span><span class="sxs-lookup"><span data-stu-id="b1d2b-474">/attachments</span></span> | <span data-ttu-id="b1d2b-475">The path and name for the container that you previously created.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-475">The path and name for the container that you previously created.</span></span> <span data-ttu-id="b1d2b-476">For this example, click the folder icon, and then select the "/attachments" container.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-476">For this example, click the folder icon, and then select the "/attachments" container.</span></span> | 
   | <span data-ttu-id="b1d2b-477">**Blob name**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-477">**Blob name**</span></span> | <span data-ttu-id="b1d2b-478">**Name** field</span><span class="sxs-lookup"><span data-stu-id="b1d2b-478">**Name** field</span></span> | <span data-ttu-id="b1d2b-479">For this example, use the attachment's name as the blob's name.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-479">For this example, use the attachment's name as the blob's name.</span></span> <span data-ttu-id="b1d2b-480">Click inside this box so that the dynamic content list appears, and then select the **Name** field under the **When a new email arrives** action.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-480">Click inside this box so that the dynamic content list appears, and then select the **Name** field under the **When a new email arrives** action.</span></span> | 
   | <span data-ttu-id="b1d2b-481">**Blob content**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-481">**Blob content**</span></span> | <span data-ttu-id="b1d2b-482">**Content** field</span><span class="sxs-lookup"><span data-stu-id="b1d2b-482">**Content** field</span></span> | <span data-ttu-id="b1d2b-483">For this example, use the **Content** field as the blob content.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-483">For this example, use the **Content** field as the blob content.</span></span> <span data-ttu-id="b1d2b-484">Click inside this box so that the dynamic content list appears, and then select **Content** under the **When a new email arrives** action.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-484">Click inside this box so that the dynamic content list appears, and then select **Content** under the **When a new email arrives** action.</span></span> |
   |||| 

   <span data-ttu-id="b1d2b-485">When you're done, the action looks like this example:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-485">When you're done, the action looks like this example:</span></span>

   ![Finished "Create blob" action](./media/tutorial-process-email-attachments-workflow/create-blob-per-attachment-done.png)

5. <span data-ttu-id="b1d2b-487">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-487">Save your logic app.</span></span> 

### <a name="check-attachment-handling"></a><span data-ttu-id="b1d2b-488">Check attachment handling</span><span class="sxs-lookup"><span data-stu-id="b1d2b-488">Check attachment handling</span></span>

<span data-ttu-id="b1d2b-489">Next, test whether your logic app handles the attachments the way that you specified:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-489">Next, test whether your logic app handles the attachments the way that you specified:</span></span>

1. <span data-ttu-id="b1d2b-490">If your logic app isn't running already, choose **Run** on the designer toolbar.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-490">If your logic app isn't running already, choose **Run** on the designer toolbar.</span></span>

2. <span data-ttu-id="b1d2b-491">Send yourself an email that meets this criteria:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-491">Send yourself an email that meets this criteria:</span></span>

   * <span data-ttu-id="b1d2b-492">Your email's subject has the text that you specified in the trigger's **Subject filter**: ```Business Analyst 2 #423501```</span><span class="sxs-lookup"><span data-stu-id="b1d2b-492">Your email's subject has the text that you specified in the trigger's **Subject filter**: ```Business Analyst 2 #423501```</span></span>

   * <span data-ttu-id="b1d2b-493">Your email has at least two attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-493">Your email has at least two attachments.</span></span> 
   <span data-ttu-id="b1d2b-494">For now, just create two empty text files and attach those files to your email.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-494">For now, just create two empty text files and attach those files to your email.</span></span>

   <span data-ttu-id="b1d2b-495">If your logic app didn't trigger or run despite a successful trigger, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-495">If your logic app didn't trigger or run despite a successful trigger, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

3. <span data-ttu-id="b1d2b-496">Check that your logic app saved the email and attachments to the correct storage container.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-496">Check that your logic app saved the email and attachments to the correct storage container.</span></span> 

   1. <span data-ttu-id="b1d2b-497">In Storage Explorer, expand **(Local and Attached)** > 
   **Storage Accounts** > **attachmentstorageacct (External)** > 
   **Blob Containers** > **attachments**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-497">In Storage Explorer, expand **(Local and Attached)** > 
**Storage Accounts** > **attachmentstorageacct (External)** > 
**Blob Containers** > **attachments**.</span></span>

   2. <span data-ttu-id="b1d2b-498">Check the **attachments** container for both the email and the attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-498">Check the **attachments** container for both the email and the attachments.</span></span>

      ![Check for saved email and attachments](./media/tutorial-process-email-attachments-workflow/storage-explorer-saved-attachments.png)

   3. <span data-ttu-id="b1d2b-500">When you're done, delete the email and attachments in Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-500">When you're done, delete the email and attachments in Storage Explorer.</span></span>

<span data-ttu-id="b1d2b-501">Next, add an action so that your logic app sends email to review the attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-501">Next, add an action so that your logic app sends email to review the attachments.</span></span>

## <a name="send-email-notifications"></a><span data-ttu-id="b1d2b-502">Send email notifications</span><span class="sxs-lookup"><span data-stu-id="b1d2b-502">Send email notifications</span></span>

1. <span data-ttu-id="b1d2b-503">In the **if true** branch, under the **For each email attachment** loop, choose **Add an action**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-503">In the **if true** branch, under the **For each email attachment** loop, choose **Add an action**.</span></span> 

   ![Add action under "for each" loop](./media/tutorial-process-email-attachments-workflow/add-action-send-email.png)

2. <span data-ttu-id="b1d2b-505">In the search box, enter "send email" as your filter, and then select the "send email" action for your email provider.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-505">In the search box, enter "send email" as your filter, and then select the "send email" action for your email provider.</span></span> 

   <span data-ttu-id="b1d2b-506">To filter the actions list to a specific service, you can select the connector first.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-506">To filter the actions list to a specific service, you can select the connector first.</span></span>

   ![Select "send email" action for your email provider](./media/tutorial-process-email-attachments-workflow/add-action-select-send-email.png)

   * <span data-ttu-id="b1d2b-508">For Azure work or school accounts, select Office 365 Outlook.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-508">For Azure work or school accounts, select Office 365 Outlook.</span></span> 
   * <span data-ttu-id="b1d2b-509">For personal Microsoft accounts, select Outlook.com.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-509">For personal Microsoft accounts, select Outlook.com.</span></span> 

3. <span data-ttu-id="b1d2b-510">If you're asked for credentials, sign in to your email account so that Logic Apps creates a connection to your email account.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-510">If you're asked for credentials, sign in to your email account so that Logic Apps creates a connection to your email account.</span></span>

4. <span data-ttu-id="b1d2b-511">Rename the **Send an email** action with this description: ```Send email for review```</span><span class="sxs-lookup"><span data-stu-id="b1d2b-511">Rename the **Send an email** action with this description: ```Send email for review```</span></span>

5. <span data-ttu-id="b1d2b-512">Provide the information for this action and select the fields you want to include in the email as shown and described.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-512">Provide the information for this action and select the fields you want to include in the email as shown and described.</span></span> <span data-ttu-id="b1d2b-513">To add blank lines in an edit box, press Shift + Enter.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-513">To add blank lines in an edit box, press Shift + Enter.</span></span>  

   ![Send email notification](./media/tutorial-process-email-attachments-workflow/send-email-notification.png)

   <span data-ttu-id="b1d2b-515">If you can't find an expected field in the dynamic content list, choose **See more** next to **When a new email arrives**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-515">If you can't find an expected field in the dynamic content list, choose **See more** next to **When a new email arrives**.</span></span> 

   | <span data-ttu-id="b1d2b-516">Setting</span><span class="sxs-lookup"><span data-stu-id="b1d2b-516">Setting</span></span> | <span data-ttu-id="b1d2b-517">Value</span><span class="sxs-lookup"><span data-stu-id="b1d2b-517">Value</span></span> | <span data-ttu-id="b1d2b-518">Notes</span><span class="sxs-lookup"><span data-stu-id="b1d2b-518">Notes</span></span> | 
   | ------- | ----- | ----- | 
   | <span data-ttu-id="b1d2b-519">**Body**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-519">**Body**</span></span> | ```Please review new applicant:``` <p><span data-ttu-id="b1d2b-520">```Applicant name: ``` **From**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-520">```Applicant name: ``` **From**</span></span> <p><span data-ttu-id="b1d2b-521">```Application file location: ``` **Path**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-521">```Application file location: ``` **Path**</span></span> <p><span data-ttu-id="b1d2b-522">```Application email content: ``` **Body**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-522">```Application email content: ``` **Body**</span></span> | <span data-ttu-id="b1d2b-523">The email's body content.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-523">The email's body content.</span></span> <span data-ttu-id="b1d2b-524">Click inside this box, enter the example text, and from the dynamic content list, select these fields:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-524">Click inside this box, enter the example text, and from the dynamic content list, select these fields:</span></span> <p><span data-ttu-id="b1d2b-525">- The **From** field under **When a new email arrives**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-525">- The **From** field under **When a new email arrives**</span></span> </br><span data-ttu-id="b1d2b-526">- The **Path** field under **Create blob for email body**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-526">- The **Path** field under **Create blob for email body**</span></span> </br><span data-ttu-id="b1d2b-527">- The **Body** field under **Call RemoveHTMLFunction to clean email body**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-527">- The **Body** field under **Call RemoveHTMLFunction to clean email body**</span></span> | 
   | <span data-ttu-id="b1d2b-528">**Subject**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-528">**Subject**</span></span>  | <span data-ttu-id="b1d2b-529">```ASAP - Review applicant for position: ``` **Subject**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-529">```ASAP - Review applicant for position: ``` **Subject**</span></span> | <span data-ttu-id="b1d2b-530">The email subject that you want to include.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-530">The email subject that you want to include.</span></span> <span data-ttu-id="b1d2b-531">Click inside this box, enter the example text, and from the dynamic content list, select the **Subject** field under **When a new email arrives**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-531">Click inside this box, enter the example text, and from the dynamic content list, select the **Subject** field under **When a new email arrives**.</span></span> | 
   | <span data-ttu-id="b1d2b-532">**To**</span><span class="sxs-lookup"><span data-stu-id="b1d2b-532">**To**</span></span> | <span data-ttu-id="b1d2b-533"><*recipient-email-address*></span><span class="sxs-lookup"><span data-stu-id="b1d2b-533"><*recipient-email-address*></span></span> | <span data-ttu-id="b1d2b-534">For testing purposes, you can use your own email address.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-534">For testing purposes, you can use your own email address.</span></span> | 
   |||| 

   > [!NOTE] 
   > <span data-ttu-id="b1d2b-535">If you select a field that contains an array, such as the **Content** field, which is an array that contains attachments, the designer automatically adds a "For each" loop around the action that references that field.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-535">If you select a field that contains an array, such as the **Content** field, which is an array that contains attachments, the designer automatically adds a "For each" loop around the action that references that field.</span></span> <span data-ttu-id="b1d2b-536">That way, your logic app can perform that action on each array item.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-536">That way, your logic app can perform that action on each array item.</span></span> <span data-ttu-id="b1d2b-537">To remove the loop, remove the field for the array, move the referencing action to outside the loop, choose the ellipses (**...**) on the loop's title bar, and choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-537">To remove the loop, remove the field for the array, move the referencing action to outside the loop, choose the ellipses (**...**) on the loop's title bar, and choose **Delete**.</span></span>
     
6. <span data-ttu-id="b1d2b-538">Save your logic app.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-538">Save your logic app.</span></span> 

<span data-ttu-id="b1d2b-539">Now, test your logic app, which now looks like this example:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-539">Now, test your logic app, which now looks like this example:</span></span>

![Finished logic app](./media/tutorial-process-email-attachments-workflow/complete.png)

## <a name="run-your-logic-app"></a><span data-ttu-id="b1d2b-541">Run your logic app</span><span class="sxs-lookup"><span data-stu-id="b1d2b-541">Run your logic app</span></span>

1. <span data-ttu-id="b1d2b-542">Send yourself an email that meets this criteria:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-542">Send yourself an email that meets this criteria:</span></span>

   * <span data-ttu-id="b1d2b-543">Your email's subject has the text that you specified in the trigger's **Subject filter**: ```Business Analyst 2 #423501```</span><span class="sxs-lookup"><span data-stu-id="b1d2b-543">Your email's subject has the text that you specified in the trigger's **Subject filter**: ```Business Analyst 2 #423501```</span></span>

   * <span data-ttu-id="b1d2b-544">Your email has at one or more attachments.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-544">Your email has at one or more attachments.</span></span> 
   <span data-ttu-id="b1d2b-545">You can reuse an empty text file from your previous test.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-545">You can reuse an empty text file from your previous test.</span></span> 
   <span data-ttu-id="b1d2b-546">For a more realistic scenario, attach a resume file.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-546">For a more realistic scenario, attach a resume file.</span></span>

   * <span data-ttu-id="b1d2b-547">The email body has this text, which you can copy and paste:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-547">The email body has this text, which you can copy and paste:</span></span>

     ```
     Name: Jamal Hartnett   
     
     Street address: 12345 Anywhere Road   
     
     City: Any Town   
     
     State or Country: Any State   
     
     Postal code: 00000   
     
     Email address: jamhartnett@outlook.com   
     
     Phone number: 000-000-0000   
     
     Position: Business Analyst 2 #423501   

     Technical skills: Dynamics CRM, MySQL, Microsoft SQL Server, JavaScript, Perl, Power BI, Tableau, Microsoft Office: Excel, Visio, Word, PowerPoint, SharePoint, and Outlook   

     Professional skills: Data, process, workflow, statistics, risk analysis, modeling; technical writing, expert communicator and presenter, logical and analytical thinker, team builder, mediator, negotiator, self-starter, self-managing  
     
     Certifications: Six Sigma Green Belt, Lean Project Management   
     
     Language skills: English, Mandarin, Spanish   
     
     Education: Master of Business Administration   
     ```

2. <span data-ttu-id="b1d2b-548">Run your logic app.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-548">Run your logic app.</span></span> <span data-ttu-id="b1d2b-549">If successful, your logic app sends you an email that looks like this example:</span><span class="sxs-lookup"><span data-stu-id="b1d2b-549">If successful, your logic app sends you an email that looks like this example:</span></span>

   ![Email notification sent by logic app](./media/tutorial-process-email-attachments-workflow/email-notification.png)

   <span data-ttu-id="b1d2b-551">If you don't get any emails, check your email's junk folder.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-551">If you don't get any emails, check your email's junk folder.</span></span> 
   <span data-ttu-id="b1d2b-552">Your email junk filter might redirect these kinds of mails.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-552">Your email junk filter might redirect these kinds of mails.</span></span> 
   <span data-ttu-id="b1d2b-553">Otherwise, if you're unsure that your logic app ran correctly, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-553">Otherwise, if you're unsure that your logic app ran correctly, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

<span data-ttu-id="b1d2b-554">Congratulations, you've now created and run a logic app that automates tasks across different Azure services and calls some custom code.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-554">Congratulations, you've now created and run a logic app that automates tasks across different Azure services and calls some custom code.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="b1d2b-555">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="b1d2b-555">Clean up resources</span></span>

<span data-ttu-id="b1d2b-556">When no longer needed, delete the resource group that contains your logic app and related resources.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-556">When no longer needed, delete the resource group that contains your logic app and related resources.</span></span> <span data-ttu-id="b1d2b-557">On the main Azure menu, go to **Resource groups**, and then select the resource group for your logic app.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-557">On the main Azure menu, go to **Resource groups**, and then select the resource group for your logic app.</span></span> <span data-ttu-id="b1d2b-558">Choose **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-558">Choose **Delete resource group**.</span></span> <span data-ttu-id="b1d2b-559">Enter the resource group name as confirmation, and choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-559">Enter the resource group name as confirmation, and choose **Delete**.</span></span>

![Delete logic app resource group](./media/tutorial-process-email-attachments-workflow/delete-resource-group.png)

## <a name="get-support"></a><span data-ttu-id="b1d2b-561">Get support</span><span class="sxs-lookup"><span data-stu-id="b1d2b-561">Get support</span></span>

* <span data-ttu-id="b1d2b-562">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-562">For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>
* <span data-ttu-id="b1d2b-563">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="b1d2b-563">To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1d2b-564">Next steps</span><span class="sxs-lookup"><span data-stu-id="b1d2b-564">Next steps</span></span>

<span data-ttu-id="b1d2b-565">In this tutorial, you created a logic app that processes and stores email attachments by integrating Azure services, such as Azure Storage and Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-565">In this tutorial, you created a logic app that processes and stores email attachments by integrating Azure services, such as Azure Storage and Azure Functions.</span></span> <span data-ttu-id="b1d2b-566">Now, learn more about other connectors that you can use to build logic apps.</span><span class="sxs-lookup"><span data-stu-id="b1d2b-566">Now, learn more about other connectors that you can use to build logic apps.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b1d2b-567">Learn more about connectors for Logic Apps</span><span class="sxs-lookup"><span data-stu-id="b1d2b-567">Learn more about connectors for Logic Apps</span></span>](../connectors/apis-list.md)
