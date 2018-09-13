---
title: Manage Key Vault in Azure Stack using PowerShell | Microsoft Docs
description: Learn how to manage Key Vault in Azure Stack using PowerShell.
services: azure-stack
documentationcenter: ''
author: SnehaGunda
manager: byronr
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: sngun
ms.openlocfilehash: afc4519d355eba560a647d4c1f903b1e29f2e06e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550749"
---
# <a name="manage-key-vault-in-azure-stack-using-the-portal"></a><span data-ttu-id="cd672-103">Manage Key Vault in Azure Stack using the portal</span><span class="sxs-lookup"><span data-stu-id="cd672-103">Manage Key Vault in Azure Stack using the portal</span></span>

<span data-ttu-id="cd672-104">Starting in Technical Preview 3 (TP3), you can manage Key Vault in Azure Stack by using the Azure Stack portal.</span><span class="sxs-lookup"><span data-stu-id="cd672-104">Starting in Technical Preview 3 (TP3), you can manage Key Vault in Azure Stack by using the Azure Stack portal.</span></span> <span data-ttu-id="cd672-105">This article helps you get started to create and manage Key Vault in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="cd672-105">This article helps you get started to create and manage Key Vault in Azure Stack.</span></span> 

>[!NOTE]
> <span data-ttu-id="cd672-106">In TP3, you can create and manage a key vault from the [user portal](azure-stack-manage-portals.md#the-user-portal) or user API only.</span><span class="sxs-lookup"><span data-stu-id="cd672-106">In TP3, you can create and manage a key vault from the [user portal](azure-stack-manage-portals.md#the-user-portal) or user API only.</span></span> <span data-ttu-id="cd672-107">If you are an administrator, you should sign in to the user portal to manage key vaults, keys, and secrets.</span><span class="sxs-lookup"><span data-stu-id="cd672-107">If you are an administrator, you should sign in to the user portal to manage key vaults, keys, and secrets.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="cd672-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cd672-108">Prerequisites</span></span>  

* <span data-ttu-id="cd672-109">Azure Stack administrators must have [created an offer](azure-stack-create-offer.md) that includes the Key Vault service.</span><span class="sxs-lookup"><span data-stu-id="cd672-109">Azure Stack administrators must have [created an offer](azure-stack-create-offer.md) that includes the Key Vault service.</span></span>  
* <span data-ttu-id="cd672-110">Tenants must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that includes the Key Vault service.</span><span class="sxs-lookup"><span data-stu-id="cd672-110">Tenants must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that includes the Key Vault service.</span></span>  
 
## <a name="create-a-key-vault"></a><span data-ttu-id="cd672-111">Create a key vault</span><span class="sxs-lookup"><span data-stu-id="cd672-111">Create a key vault</span></span> 

1. <span data-ttu-id="cd672-112">Sign in to the user portal(https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="cd672-112">Sign in to the user portal(https://portal.local.azurestack.external).</span></span>  

2. <span data-ttu-id="cd672-113">From the dashboard, click **New > Security + Identity > Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="cd672-113">From the dashboard, click **New > Security + Identity > Key Vault**.</span></span>  

    ![KV screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-kv-manage-portal/image1.png)  

3. <span data-ttu-id="cd672-115">On the **Create Key Vault** blade, assign a **Name** for your vault.</span><span class="sxs-lookup"><span data-stu-id="cd672-115">On the **Create Key Vault** blade, assign a **Name** for your vault.</span></span> <span data-ttu-id="cd672-116">Vault name can contain only alphanumeric characters, the special character hyphen (-), and it shouldn’t start with a number.</span><span class="sxs-lookup"><span data-stu-id="cd672-116">Vault name can contain only alphanumeric characters, the special character hyphen (-), and it shouldn’t start with a number.</span></span>  

4. <span data-ttu-id="cd672-117">Choose a **Subscription** from the list of available subscriptions.</span><span class="sxs-lookup"><span data-stu-id="cd672-117">Choose a **Subscription** from the list of available subscriptions.</span></span> <span data-ttu-id="cd672-118">All subscriptions that offer the Key Vault service are displayed in the drop-down.</span><span class="sxs-lookup"><span data-stu-id="cd672-118">All subscriptions that offer the Key Vault service are displayed in the drop-down.</span></span>  

5. <span data-ttu-id="cd672-119">Select an existing **Resource Group** or create a new one.</span><span class="sxs-lookup"><span data-stu-id="cd672-119">Select an existing **Resource Group** or create a new one.</span></span>  

6. <span data-ttu-id="cd672-120">Select the **Pricing tier**.</span><span class="sxs-lookup"><span data-stu-id="cd672-120">Select the **Pricing tier**.</span></span>  
    >[!NOTE]
    > <span data-ttu-id="cd672-121">At the TP3 release, key vault supports the **Standard** SKU only.</span><span class="sxs-lookup"><span data-stu-id="cd672-121">At the TP3 release, key vault supports the **Standard** SKU only.</span></span>

7. <span data-ttu-id="cd672-122">Choose an existing **Access policies** or create a new one.</span><span class="sxs-lookup"><span data-stu-id="cd672-122">Choose an existing **Access policies** or create a new one.</span></span> <span data-ttu-id="cd672-123">Access policy allows you to grant permissions for a user, application, or a security group to perform operations with this vault.</span><span class="sxs-lookup"><span data-stu-id="cd672-123">Access policy allows you to grant permissions for a user, application, or a security group to perform operations with this vault.</span></span>  

8. <span data-ttu-id="cd672-124">Optionally, choose an **Advanced access policy** to enable the features like access to Virtual Machines for deployment, access to Resource Manager for template deployment and access to Azure Disk Encryption for volume encryption.</span><span class="sxs-lookup"><span data-stu-id="cd672-124">Optionally, choose an **Advanced access policy** to enable the features like access to Virtual Machines for deployment, access to Resource Manager for template deployment and access to Azure Disk Encryption for volume encryption.</span></span> 
  
9.  <span data-ttu-id="cd672-125">After configuring the settings, click **OK** and then **Create**.</span><span class="sxs-lookup"><span data-stu-id="cd672-125">After configuring the settings, click **OK** and then **Create**.</span></span> <span data-ttu-id="cd672-126">This starts the key vault deployment.</span><span class="sxs-lookup"><span data-stu-id="cd672-126">This starts the key vault deployment.</span></span> 

## <a name="manage-keys-and-secrets"></a><span data-ttu-id="cd672-127">Manage keys and secrets</span><span class="sxs-lookup"><span data-stu-id="cd672-127">Manage keys and secrets</span></span>

<span data-ttu-id="cd672-128">After you create a vault, use the following steps to create and manage keys and secrets within the vault.</span><span class="sxs-lookup"><span data-stu-id="cd672-128">After you create a vault, use the following steps to create and manage keys and secrets within the vault.</span></span>

## <a name="create-a-key"></a><span data-ttu-id="cd672-129">Create a key</span><span class="sxs-lookup"><span data-stu-id="cd672-129">Create a key</span></span>

1. <span data-ttu-id="cd672-130">Sign in to the user portal (https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="cd672-130">Sign in to the user portal (https://portal.local.azurestack.external).</span></span>  

2. <span data-ttu-id="cd672-131">From the dashboard, click **All resources** > select the key vault that you created earlier> click the **Keys** tile.</span><span class="sxs-lookup"><span data-stu-id="cd672-131">From the dashboard, click **All resources** > select the key vault that you created earlier> click the **Keys** tile.</span></span>  

3. <span data-ttu-id="cd672-132">From the **Keys** blade, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="cd672-132">From the **Keys** blade, click **Add**.</span></span> 

4. <span data-ttu-id="cd672-133">On the **Create a key** blade, form the list of **Options**, choose the method that you want to use to create a key.</span><span class="sxs-lookup"><span data-stu-id="cd672-133">On the **Create a key** blade, form the list of **Options**, choose the method that you want to use to create a key.</span></span> <span data-ttu-id="cd672-134">You can **Generate** a new key, **Upload** an existing key, or **Restore Backup** key.</span><span class="sxs-lookup"><span data-stu-id="cd672-134">You can **Generate** a new key, **Upload** an existing key, or **Restore Backup** key.</span></span>  

5. <span data-ttu-id="cd672-135">Enter a **Name** for your key.</span><span class="sxs-lookup"><span data-stu-id="cd672-135">Enter a **Name** for your key.</span></span> <span data-ttu-id="cd672-136">The key name can contain only alphanumeric characters and the special character hyphen (-).</span><span class="sxs-lookup"><span data-stu-id="cd672-136">The key name can contain only alphanumeric characters and the special character hyphen (-).</span></span>  

6. <span data-ttu-id="cd672-137">Optionally, configure **Set activation date** and **Set expiration date** values for your key.</span><span class="sxs-lookup"><span data-stu-id="cd672-137">Optionally, configure **Set activation date** and **Set expiration date** values for your key.</span></span>  

7. <span data-ttu-id="cd672-138">Click **Create** to start the deployment.</span><span class="sxs-lookup"><span data-stu-id="cd672-138">Click **Create** to start the deployment.</span></span>  

<span data-ttu-id="cd672-139">After the key is successfully created, you can select it from the **Keys** blade and view or modify its properties.</span><span class="sxs-lookup"><span data-stu-id="cd672-139">After the key is successfully created, you can select it from the **Keys** blade and view or modify its properties.</span></span> <span data-ttu-id="cd672-140">The properties section contains the **Key Identifier**, a URI by which external applications can access this key.</span><span class="sxs-lookup"><span data-stu-id="cd672-140">The properties section contains the **Key Identifier**, a URI by which external applications can access this key.</span></span> <span data-ttu-id="cd672-141">To limit operations on this key, configure settings under **Permitted operations**.</span><span class="sxs-lookup"><span data-stu-id="cd672-141">To limit operations on this key, configure settings under **Permitted operations**.</span></span>

![URI key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-kv-manage-portal/image4.png)  

## <a name="create-a-secret"></a><span data-ttu-id="cd672-143">Create a secret</span><span class="sxs-lookup"><span data-stu-id="cd672-143">Create a secret</span></span> 

1. <span data-ttu-id="cd672-144">Sign in to the user portal (https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="cd672-144">Sign in to the user portal (https://portal.local.azurestack.external).</span></span>  
2. <span data-ttu-id="cd672-145">From the dashboard, click **All resources** > select the key vault that you created earlier> click the **Secrets** tile.</span><span class="sxs-lookup"><span data-stu-id="cd672-145">From the dashboard, click **All resources** > select the key vault that you created earlier> click the **Secrets** tile.</span></span>  

3. <span data-ttu-id="cd672-146">From the **Secrets** blade, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="cd672-146">From the **Secrets** blade, click **Add**.</span></span>  

4. <span data-ttu-id="cd672-147">On the **Create a secret** blade, from the list of **Upload options**, choose an option by which you want to create a secret.</span><span class="sxs-lookup"><span data-stu-id="cd672-147">On the **Create a secret** blade, from the list of **Upload options**, choose an option by which you want to create a secret.</span></span> <span data-ttu-id="cd672-148">You can create a secret **Manually** by entering a value for the secret, or by uploading a **Certificate** from your local machine.</span><span class="sxs-lookup"><span data-stu-id="cd672-148">You can create a secret **Manually** by entering a value for the secret, or by uploading a **Certificate** from your local machine.</span></span>  

5. <span data-ttu-id="cd672-149">Enter a **Name** for the secret.</span><span class="sxs-lookup"><span data-stu-id="cd672-149">Enter a **Name** for the secret.</span></span> <span data-ttu-id="cd672-150">The secret name can contain only alphanumeric characters and the special character hyphen (-).</span><span class="sxs-lookup"><span data-stu-id="cd672-150">The secret name can contain only alphanumeric characters and the special character hyphen (-).</span></span>  

6. <span data-ttu-id="cd672-151">Optionally, specify the **Content type**, and configure values for **Set activation date** and **Set expiration date** values for the secret.</span><span class="sxs-lookup"><span data-stu-id="cd672-151">Optionally, specify the **Content type**, and configure values for **Set activation date** and **Set expiration date** values for the secret.</span></span>  

7. <span data-ttu-id="cd672-152">Click Create to start the deployment.</span><span class="sxs-lookup"><span data-stu-id="cd672-152">Click Create to start the deployment.</span></span>  

<span data-ttu-id="cd672-153">After the secret is successfully created, you can select it from the **Secrets** blade and view or modify its properties.</span><span class="sxs-lookup"><span data-stu-id="cd672-153">After the secret is successfully created, you can select it from the **Secrets** blade and view or modify its properties.</span></span> <span data-ttu-id="cd672-154">The properties section contains **Secret Identifier**, a URI by which external applications can access this secret.</span><span class="sxs-lookup"><span data-stu-id="cd672-154">The properties section contains **Secret Identifier**, a URI by which external applications can access this secret.</span></span> 

![URI secret](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-kv-manage-portal/image5.png) 


## <a name="next-steps"></a><span data-ttu-id="cd672-156">Next Steps</span><span class="sxs-lookup"><span data-stu-id="cd672-156">Next Steps</span></span>
* [<span data-ttu-id="cd672-157">Deploy a VM by retrieving the password stored in a key vault</span><span class="sxs-lookup"><span data-stu-id="cd672-157">Deploy a VM by retrieving the password stored in a key vault</span></span>](azure-stack-kv-deploy-vm-with-secret.md)  
* [<span data-ttu-id="cd672-158">Deploy a VM with certificate stored in a key vault</span><span class="sxs-lookup"><span data-stu-id="cd672-158">Deploy a VM with certificate stored in a key vault</span></span>](azure-stack-kv-push-secret-into-vm.md)     





