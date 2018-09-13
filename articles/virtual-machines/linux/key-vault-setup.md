---
title: Set up Azure Key Vault for Linux VMs | Microsoft Docs
description: How to set up Key Vault for use with an Azure Resource Manager virtual machine with the CLI 2.0.
services: virtual-machines-linux
documentationcenter: ''
author: singhkays
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 782bb535991343a5951b6413bee11495ccb1441c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825799"
---
# <a name="how-to-set-up-key-vault-for-virtual-machines-with-the-azure-cli-20"></a><span data-ttu-id="346c0-103">How to set up Key Vault for virtual machines with the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="346c0-103">How to set up Key Vault for virtual machines with the Azure CLI 2.0</span></span>

<span data-ttu-id="346c0-104">In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span><span class="sxs-lookup"><span data-stu-id="346c0-104">In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span></span> <span data-ttu-id="346c0-105">To learn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="346c0-105">To learn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="346c0-106">In order for Key Vault to be used with Azure Resource Manager VMs, the *EnabledForDeployment* property on Key Vault must be set to true.</span><span class="sxs-lookup"><span data-stu-id="346c0-106">In order for Key Vault to be used with Azure Resource Manager VMs, the *EnabledForDeployment* property on Key Vault must be set to true.</span></span> <span data-ttu-id="346c0-107">This article shows you how to set up Key Vault for use with Azure virtual machines (VMs) using the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="346c0-107">This article shows you how to set up Key Vault for use with Azure virtual machines (VMs) using the Azure CLI 2.0.</span></span> 

<span data-ttu-id="346c0-108">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span><span class="sxs-lookup"><span data-stu-id="346c0-108">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/reference-index#az_login).</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="346c0-109">Create a Key Vault</span><span class="sxs-lookup"><span data-stu-id="346c0-109">Create a Key Vault</span></span>
<span data-ttu-id="346c0-110">Create a key vault and assign the deployment policy with [az keyvault create](/cli/azure/keyvault#az_keyvault_create).</span><span class="sxs-lookup"><span data-stu-id="346c0-110">Create a key vault and assign the deployment policy with [az keyvault create](/cli/azure/keyvault#az_keyvault_create).</span></span> <span data-ttu-id="346c0-111">The following example creates a key vault named `myKeyVault` in the `myResourceGroup` resource group:</span><span class="sxs-lookup"><span data-stu-id="346c0-111">The following example creates a key vault named `myKeyVault` in the `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a><span data-ttu-id="346c0-112">Update a Key Vault for use with VMs</span><span class="sxs-lookup"><span data-stu-id="346c0-112">Update a Key Vault for use with VMs</span></span>
<span data-ttu-id="346c0-113">Set the deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#az_keyvault_update).</span><span class="sxs-lookup"><span data-stu-id="346c0-113">Set the deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#az_keyvault_update).</span></span> <span data-ttu-id="346c0-114">The following updates the key vault named `myKeyVault` in the `myResourceGroup` resource group:</span><span class="sxs-lookup"><span data-stu-id="346c0-114">The following updates the key vault named `myKeyVault` in the `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="346c0-115">Use templates to set up Key Vault</span><span class="sxs-lookup"><span data-stu-id="346c0-115">Use templates to set up Key Vault</span></span>
<span data-ttu-id="346c0-116">When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource as follows:</span><span class="sxs-lookup"><span data-stu-id="346c0-116">When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource as follows:</span></span>

```json
{
    "type": "Microsoft.KeyVault/vaults",
    "name": "ContosoKeyVault",
    "apiVersion": "2015-06-01",
    "location": "<location-of-key-vault>",
    "properties": {
    "enabledForDeployment": "true",
    ....
    ....
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="346c0-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="346c0-117">Next steps</span></span>
<span data-ttu-id="346c0-118">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="346c0-118">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
