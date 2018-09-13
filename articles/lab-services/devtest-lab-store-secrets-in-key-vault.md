---
title: Store secrets in a key vault in Azure DevTest Labs | Microsoft Docs
description: Learn how to store secrets in an Azure Key Vault and use them while creating a VM, formula, or an environment.
services: devtest-lab
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.assetid: ''
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2018
ms.author: spelluru
ms.openlocfilehash: d87c8a46459a9b4bf80bef895ec97e436d38e699
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870774"
---
# <a name="store-secrets-in-a-key-vault-in-azure-devtest-labs"></a><span data-ttu-id="9199d-103">Store secrets in a key vault in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="9199d-103">Store secrets in a key vault in Azure DevTest Labs</span></span>
<span data-ttu-id="9199d-104">You may need to enter a complex secret when using Azure DevTest Labs: password for your Windows VM, public SSH key for your Linux VM, or personal access token to clone your Git repo through an artifact.</span><span class="sxs-lookup"><span data-stu-id="9199d-104">You may need to enter a complex secret when using Azure DevTest Labs: password for your Windows VM, public SSH key for your Linux VM, or personal access token to clone your Git repo through an artifact.</span></span> <span data-ttu-id="9199d-105">Secrets are usually long and have random characters.</span><span class="sxs-lookup"><span data-stu-id="9199d-105">Secrets are usually long and have random characters.</span></span> <span data-ttu-id="9199d-106">Therefore, entering them can be tricky and inconvenient, especially if you use the same secret multiple times.</span><span class="sxs-lookup"><span data-stu-id="9199d-106">Therefore, entering them can be tricky and inconvenient, especially if you use the same secret multiple times.</span></span>

<span data-ttu-id="9199d-107">To solve this problem and also keep your secrets in a safe place, DevTest Labs supports storing secrets in an [Azure key vault](../key-vault/key-vault-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9199d-107">To solve this problem and also keep your secrets in a safe place, DevTest Labs supports storing secrets in an [Azure key vault](../key-vault/key-vault-overview.md).</span></span> <span data-ttu-id="9199d-108">When a user saves a secret for the first time, the DevTest Labs service automatically creates a key vault in the same resource group that contains the lab and stores the secret in the key vault.</span><span class="sxs-lookup"><span data-stu-id="9199d-108">When a user saves a secret for the first time, the DevTest Labs service automatically creates a key vault in the same resource group that contains the lab and stores the secret in the key vault.</span></span> <span data-ttu-id="9199d-109">DevTest Labs creates a separate key vault for each user.</span><span class="sxs-lookup"><span data-stu-id="9199d-109">DevTest Labs creates a separate key vault for each user.</span></span> 

## <a name="save-a-secret-in-azure-key-vault"></a><span data-ttu-id="9199d-110">Save a secret in Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="9199d-110">Save a secret in Azure Key Vault</span></span>
<span data-ttu-id="9199d-111">To save your secret in Azure Key Vault, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="9199d-111">To save your secret in Azure Key Vault, do the following steps:</span></span>

1. <span data-ttu-id="9199d-112">Select **My secrets** on the left menu.</span><span class="sxs-lookup"><span data-stu-id="9199d-112">Select **My secrets** on the left menu.</span></span>
2. <span data-ttu-id="9199d-113">Enter a **name** for the secret.</span><span class="sxs-lookup"><span data-stu-id="9199d-113">Enter a **name** for the secret.</span></span> <span data-ttu-id="9199d-114">You see this name in the drop-down list when creating a VM, formula, or an environment.</span><span class="sxs-lookup"><span data-stu-id="9199d-114">You see this name in the drop-down list when creating a VM, formula, or an environment.</span></span> 
3. <span data-ttu-id="9199d-115">Enter the secret as the **value**.</span><span class="sxs-lookup"><span data-stu-id="9199d-115">Enter the secret as the **value**.</span></span>

    ![Store secret](media/devtest-lab-store-secrets-in-key-vault/store-secret.png)

## <a name="use-a-secret-from-azure-key-vault"></a><span data-ttu-id="9199d-117">Use a secret from Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="9199d-117">Use a secret from Azure Key Vault</span></span>
<span data-ttu-id="9199d-118">When you need to enter a secret to create a VM, formula, or an environment, you can either enter a secret manually or select a saved secret from the key vault.</span><span class="sxs-lookup"><span data-stu-id="9199d-118">When you need to enter a secret to create a VM, formula, or an environment, you can either enter a secret manually or select a saved secret from the key vault.</span></span> <span data-ttu-id="9199d-119">To use a secret stored in your key vault, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="9199d-119">To use a secret stored in your key vault, do the following actions:</span></span>

1. <span data-ttu-id="9199d-120">Select **Use a saved secret**.</span><span class="sxs-lookup"><span data-stu-id="9199d-120">Select **Use a saved secret**.</span></span> 
2. <span data-ttu-id="9199d-121">Select your secret from the drop-down list for **Pick a secret**.</span><span class="sxs-lookup"><span data-stu-id="9199d-121">Select your secret from the drop-down list for **Pick a secret**.</span></span> 

    ![Use secret in VM](media/devtest-lab-store-secrets-in-key-vault/secret-store-pick-a-secret.png)

## <a name="use-a-secret-in-an-azure-resource-manager-template"></a><span data-ttu-id="9199d-123">Use a secret in an Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="9199d-123">Use a secret in an Azure Resource Manager template</span></span>
<span data-ttu-id="9199d-124">You can specify your secret name in an Azure Resource Manager template that's used to create a VM as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="9199d-124">You can specify your secret name in an Azure Resource Manager template that's used to create a VM as shown in the following example:</span></span>

![Use secret in formula or environment](media/devtest-lab-store-secrets-in-key-vault/secret-store-arm-template.png)

## <a name="next-steps"></a><span data-ttu-id="9199d-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="9199d-126">Next steps</span></span>

- [<span data-ttu-id="9199d-127">Create a VM using the secret</span><span class="sxs-lookup"><span data-stu-id="9199d-127">Create a VM using the secret</span></span>](devtest-lab-add-vm.md) 
- [<span data-ttu-id="9199d-128">Create a formula using the secret</span><span class="sxs-lookup"><span data-stu-id="9199d-128">Create a formula using the secret</span></span>](devtest-lab-manage-formulas.md)
- [<span data-ttu-id="9199d-129">Create an environment using the secret</span><span class="sxs-lookup"><span data-stu-id="9199d-129">Create an environment using the secret</span></span>](devtest-lab-create-environment-from-arm.md)
