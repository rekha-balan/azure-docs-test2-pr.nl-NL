---
title: Manage Key Vault in Azure Stack by using the portal | Microsoft Docs
description: Learn how to manage Key Vault in Azure Stack by using the portal
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: D4300668-461F-45F6-BF3B-33B502C39D17
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2018
ms.author: sethm
ms.openlocfilehash: 91035f84d02810d838127ecf6a2f6424ef5df6cf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858054"
---
# <a name="manage-key-vault-in-azure-stack-by-using-the-portal"></a><span data-ttu-id="2a6e5-103">Manage Key Vault in Azure Stack by using the portal</span><span class="sxs-lookup"><span data-stu-id="2a6e5-103">Manage Key Vault in Azure Stack by using the portal</span></span>

<span data-ttu-id="2a6e5-104">You can manage Key Vault in Azure Stack by using the Azure Stack portal.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-104">You can manage Key Vault in Azure Stack by using the Azure Stack portal.</span></span> <span data-ttu-id="2a6e5-105">This article helps you get started to create and manage a key vault in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-105">This article helps you get started to create and manage a key vault in Azure Stack.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a6e5-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2a6e5-106">Prerequisites</span></span>

<span data-ttu-id="2a6e5-107">You must subscribe to an offer that includes the Azure Key Vault service.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-107">You must subscribe to an offer that includes the Azure Key Vault service.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="2a6e5-108">Create a key vault</span><span class="sxs-lookup"><span data-stu-id="2a6e5-108">Create a key vault</span></span>

1. <span data-ttu-id="2a6e5-109">Sign in to the [user portal](https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="2a6e5-109">Sign in to the [user portal](https://portal.local.azurestack.external).</span></span>

2. <span data-ttu-id="2a6e5-110">From the dashboard, select **New** > **Security + Identity** > **Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-110">From the dashboard, select **New** > **Security + Identity** > **Key Vault**.</span></span>

    ![Key Vault screen](media/azure-stack-kv-manage-portal/image1.png)

3. <span data-ttu-id="2a6e5-112">In the **Create Key Vault** pane, assign a **Name** for your vault.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-112">In the **Create Key Vault** pane, assign a **Name** for your vault.</span></span> <span data-ttu-id="2a6e5-113">Vault names can contain only alphanumeric characters and the special-character hyphen (-).</span><span class="sxs-lookup"><span data-stu-id="2a6e5-113">Vault names can contain only alphanumeric characters and the special-character hyphen (-).</span></span> <span data-ttu-id="2a6e5-114">They shouldn’t start with a number.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-114">They shouldn’t start with a number.</span></span>

4. <span data-ttu-id="2a6e5-115">Choose a **Subscription** from the list of available subscriptions.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-115">Choose a **Subscription** from the list of available subscriptions.</span></span> <span data-ttu-id="2a6e5-116">All subscriptions that offer the Key Vault service are displayed in the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-116">All subscriptions that offer the Key Vault service are displayed in the drop-down list.</span></span>

5. <span data-ttu-id="2a6e5-117">Select an existing **Resource Group** or create a new one.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-117">Select an existing **Resource Group** or create a new one.</span></span>

6. <span data-ttu-id="2a6e5-118">Select the **Pricing tier**.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-118">Select the **Pricing tier**.</span></span>
    >[!NOTE]
    > <span data-ttu-id="2a6e5-119">Key vaults in the Azure Stack Development Kit support **Standard** SKUs only.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-119">Key vaults in the Azure Stack Development Kit support **Standard** SKUs only.</span></span>

7. <span data-ttu-id="2a6e5-120">Choose one of the existing **Access policies** or create a new one.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-120">Choose one of the existing **Access policies** or create a new one.</span></span> <span data-ttu-id="2a6e5-121">An access policy allows you to grant permissions for a user, application, or a security group to perform operations with this vault.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-121">An access policy allows you to grant permissions for a user, application, or a security group to perform operations with this vault.</span></span>

8. <span data-ttu-id="2a6e5-122">Optionally, choose an **Advanced access policy** to enable access to features.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-122">Optionally, choose an **Advanced access policy** to enable access to features.</span></span> <span data-ttu-id="2a6e5-123">For example: virtual machines (VMs) for deployment, Resource Manager for template deployment, and access to Azure Disk Encryption for volume encryption.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-123">For example: virtual machines (VMs) for deployment, Resource Manager for template deployment, and access to Azure Disk Encryption for volume encryption.</span></span>

9. <span data-ttu-id="2a6e5-124">After you configure the settings, select **OK**, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-124">After you configure the settings, select **OK**, and then select **Create**.</span></span> <span data-ttu-id="2a6e5-125">This starts the key vault deployment.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-125">This starts the key vault deployment.</span></span>

## <a name="manage-keys-and-secrets"></a><span data-ttu-id="2a6e5-126">Manage keys and secrets</span><span class="sxs-lookup"><span data-stu-id="2a6e5-126">Manage keys and secrets</span></span>

<span data-ttu-id="2a6e5-127">After you create a vault, use the following steps to create and manage keys and secrets within the vault.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-127">After you create a vault, use the following steps to create and manage keys and secrets within the vault.</span></span>

### <a name="create-a-key"></a><span data-ttu-id="2a6e5-128">Create a key</span><span class="sxs-lookup"><span data-stu-id="2a6e5-128">Create a key</span></span>

1. <span data-ttu-id="2a6e5-129">Sign in to the [user portal](https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="2a6e5-129">Sign in to the [user portal](https://portal.local.azurestack.external).</span></span>

2. <span data-ttu-id="2a6e5-130">From the dashboard, select **All resources**, select the key vault that you created earlier, and then select the **Keys** tile.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-130">From the dashboard, select **All resources**, select the key vault that you created earlier, and then select the **Keys** tile.</span></span>

3. <span data-ttu-id="2a6e5-131">In the **Keys** pane, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-131">In the **Keys** pane, select **Add**.</span></span>

4. <span data-ttu-id="2a6e5-132">In the **Create a key** pane, from the list of **Options**, choose the method that you want to use to create a key.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-132">In the **Create a key** pane, from the list of **Options**, choose the method that you want to use to create a key.</span></span> <span data-ttu-id="2a6e5-133">You can **Generate** a new key, **Upload** an existing key, or use **Restore Backup** to select a backup of a key.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-133">You can **Generate** a new key, **Upload** an existing key, or use **Restore Backup** to select a backup of a key.</span></span>

5. <span data-ttu-id="2a6e5-134">Enter a **Name** for your key.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-134">Enter a **Name** for your key.</span></span> <span data-ttu-id="2a6e5-135">The key name can contain only alphanumeric characters and the special character hyphen (-).</span><span class="sxs-lookup"><span data-stu-id="2a6e5-135">The key name can contain only alphanumeric characters and the special character hyphen (-).</span></span>

6. <span data-ttu-id="2a6e5-136">Optionally, configure the **Set activation date** and **Set expiration date** values for your key.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-136">Optionally, configure the **Set activation date** and **Set expiration date** values for your key.</span></span>

7. <span data-ttu-id="2a6e5-137">Select **Create** to start the deployment.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-137">Select **Create** to start the deployment.</span></span>

<span data-ttu-id="2a6e5-138">After the key is successfully created, you can select it under **Keys** and view or modify its properties.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-138">After the key is successfully created, you can select it under **Keys** and view or modify its properties.</span></span> <span data-ttu-id="2a6e5-139">The properties section contains the **Key Identifier**, which is a Uniform Resource Identifier (URI) that  external applications use to access this key.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-139">The properties section contains the **Key Identifier**, which is a Uniform Resource Identifier (URI) that  external applications use to access this key.</span></span> <span data-ttu-id="2a6e5-140">To limit operations on this key, configure the settings under **Permitted operations**.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-140">To limit operations on this key, configure the settings under **Permitted operations**.</span></span>

![URI key](media/azure-stack-kv-manage-portal/image4.png)

### <a name="create-a-secret"></a><span data-ttu-id="2a6e5-142">Create a secret</span><span class="sxs-lookup"><span data-stu-id="2a6e5-142">Create a secret</span></span>

1. <span data-ttu-id="2a6e5-143">Sign in to the [user portal](https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="2a6e5-143">Sign in to the [user portal](https://portal.local.azurestack.external).</span></span>
2. <span data-ttu-id="2a6e5-144">From the dashboard, select **All resources**, select the key vault that you created earlier, and then select the **Secrets** tile.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-144">From the dashboard, select **All resources**, select the key vault that you created earlier, and then select the **Secrets** tile.</span></span>

3. <span data-ttu-id="2a6e5-145">Under **Secrets**, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-145">Under **Secrets**, select **Add**.</span></span>

4. <span data-ttu-id="2a6e5-146">Under **Create a secret**, from the list of **Upload options**, choose an option by which you want to create a secret.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-146">Under **Create a secret**, from the list of **Upload options**, choose an option by which you want to create a secret.</span></span> <span data-ttu-id="2a6e5-147">You can create a secret **Manually** if you enter a value for the secret or upload a **Certificate** from your local machine.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-147">You can create a secret **Manually** if you enter a value for the secret or upload a **Certificate** from your local machine.</span></span>

5. <span data-ttu-id="2a6e5-148">Enter a **Name** for the secret.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-148">Enter a **Name** for the secret.</span></span> <span data-ttu-id="2a6e5-149">The secret name can contain only alphanumeric characters and the special character hyphen (-).</span><span class="sxs-lookup"><span data-stu-id="2a6e5-149">The secret name can contain only alphanumeric characters and the special character hyphen (-).</span></span>

6. <span data-ttu-id="2a6e5-150">Optionally, specify the **Content type**, and configure values for **Set activation date** and **Set expiration date** for the secret.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-150">Optionally, specify the **Content type**, and configure values for **Set activation date** and **Set expiration date** for the secret.</span></span>

7. <span data-ttu-id="2a6e5-151">Select **Create** to start the deployment.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-151">Select **Create** to start the deployment.</span></span>

<span data-ttu-id="2a6e5-152">After the secret is successfully created, you can select it under **Secrets** and view or modify its properties.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-152">After the secret is successfully created, you can select it under **Secrets** and view or modify its properties.</span></span> <span data-ttu-id="2a6e5-153">The **Secret Identifier** is a URI that external applications can use to access this secret.</span><span class="sxs-lookup"><span data-stu-id="2a6e5-153">The **Secret Identifier** is a URI that external applications can use to access this secret.</span></span>

![URI secret](media/azure-stack-kv-manage-portal/image5.png)

## <a name="next-steps"></a><span data-ttu-id="2a6e5-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="2a6e5-155">Next steps</span></span>

* [<span data-ttu-id="2a6e5-156">Deploy a VM by retrieving the password stored in Key Vault</span><span class="sxs-lookup"><span data-stu-id="2a6e5-156">Deploy a VM by retrieving the password stored in Key Vault</span></span>](azure-stack-kv-deploy-vm-with-secret.md)
* [<span data-ttu-id="2a6e5-157">Deploy a VM with certificate stored in Key Vault</span><span class="sxs-lookup"><span data-stu-id="2a6e5-157">Deploy a VM with certificate stored in Key Vault</span></span>](azure-stack-kv-push-secret-into-vm.md)
