---
title: Set up Azure Key Vault for Linux VMs | Microsoft Docs
description: How to set up Key Vault for use with an Azure Resource Manager virtual machine with the CLI 2.0.
services: virtual-machines-linux
documentationcenter: ''
author: singhkays
manager: timlt
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
ms.openlocfilehash: 8d8400c30a1bd0b31626781c1ab61ab65f60f734
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553903"
---
# <a name="how-to-set-up-key-vault-for-virtual-machines-with-the-azure-cli-20"></a><span data-ttu-id="dc245-103">How to set up Key Vault for virtual machines with the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="dc245-103">How to set up Key Vault for virtual machines with the Azure CLI 2.0</span></span>

<span data-ttu-id="dc245-104">In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span><span class="sxs-lookup"><span data-stu-id="dc245-104">In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span></span> <span data-ttu-id="dc245-105">To learn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="dc245-105">To learn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="dc245-106">In order for Key Vault to be used with Azure Resource Manager VMs, the *EnabledForDeployment* property on Key Vault must be set to true.</span><span class="sxs-lookup"><span data-stu-id="dc245-106">In order for Key Vault to be used with Azure Resource Manager VMs, the *EnabledForDeployment* property on Key Vault must be set to true.</span></span> <span data-ttu-id="dc245-107">This article shows you how to set up Key Vault for use with Azure virtual machines (VMs) using the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="dc245-107">This article shows you how to set up Key Vault for use with Azure virtual machines (VMs) using the Azure CLI 2.0.</span></span> <span data-ttu-id="dc245-108">You can also perform these steps with the [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dc245-108">You can also perform these steps with the [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="dc245-109">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="dc245-109">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="dc245-110">Create a Key Vault</span><span class="sxs-lookup"><span data-stu-id="dc245-110">Create a Key Vault</span></span>
<span data-ttu-id="dc245-111">Create a key vault and assign the deployment policy with [az keyvault create](/cli/azure/keyvault#create).</span><span class="sxs-lookup"><span data-stu-id="dc245-111">Create a key vault and assign the deployment policy with [az keyvault create](/cli/azure/keyvault#create).</span></span> <span data-ttu-id="dc245-112">The following example creates a key vault named `myKeyVault` in the `myResourceGroup` resource group:</span><span class="sxs-lookup"><span data-stu-id="dc245-112">The following example creates a key vault named `myKeyVault` in the `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a><span data-ttu-id="dc245-113">Update a Key Vault for use with VMs</span><span class="sxs-lookup"><span data-stu-id="dc245-113">Update a Key Vault for use with VMs</span></span>
<span data-ttu-id="dc245-114">Set the deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#update).</span><span class="sxs-lookup"><span data-stu-id="dc245-114">Set the deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#update).</span></span> <span data-ttu-id="dc245-115">The following updates the key vault named `myKeyVault` in the `myResourceGroup` resource group:</span><span class="sxs-lookup"><span data-stu-id="dc245-115">The following updates the key vault named `myKeyVault` in the `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="dc245-116">Use templates to set up Key Vault</span><span class="sxs-lookup"><span data-stu-id="dc245-116">Use templates to set up Key Vault</span></span>
<span data-ttu-id="dc245-117">When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource as follows:</span><span class="sxs-lookup"><span data-stu-id="dc245-117">When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource as follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="dc245-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="dc245-118">Next steps</span></span>
<span data-ttu-id="dc245-119">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="dc245-119">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
