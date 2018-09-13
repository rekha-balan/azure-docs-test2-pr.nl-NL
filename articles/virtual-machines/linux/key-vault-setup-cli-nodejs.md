---
title: Set up Key Vault for Linux VMs with the Azure CLI 1.0 | Microsoft Docs
description: How to set up Key Vault for use with an Azure Resource Manager virtual machine with the Azure CLI 1.0.
services: virtual-machines-linux
documentationcenter: ''
author: singhkays
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 9aeac01ce838afcacbc78b687689e1329b9f5ddc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564359"
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-the-azure-cli-10"></a><span data-ttu-id="8505a-103">Set up Key Vault for virtual machines in Azure Resource Manager with the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8505a-103">Set up Key Vault for virtual machines in Azure Resource Manager with the Azure CLI 1.0</span></span>
<span data-ttu-id="8505a-104">In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8505a-104">In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault.</span></span> <span data-ttu-id="8505a-105">To learn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="8505a-105">To learn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="8505a-106">In order for Key Vault to be used with Azure Resource Manager virtual machines, the *EnabledForDeployment* property on Key Vault must be set to true.</span><span class="sxs-lookup"><span data-stu-id="8505a-106">In order for Key Vault to be used with Azure Resource Manager virtual machines, the *EnabledForDeployment* property on Key Vault must be set to true.</span></span> <span data-ttu-id="8505a-107">You can do this in various clients.</span><span class="sxs-lookup"><span data-stu-id="8505a-107">You can do this in various clients.</span></span> <span data-ttu-id="8505a-108">This article shows you how to set up Key Vault for use with Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="8505a-108">This article shows you how to set up Key Vault for use with Azure Virtual Machines.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="8505a-109">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="8505a-109">CLI versions to complete the task</span></span>
<span data-ttu-id="8505a-110">You can complete the task using one of the following CLI versions</span><span class="sxs-lookup"><span data-stu-id="8505a-110">You can complete the task using one of the following CLI versions</span></span>

- <span data-ttu-id="8505a-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="8505a-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="8505a-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="8505a-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="use-cli-10-to-set-up-key-vault"></a><span data-ttu-id="8505a-113">Use CLI 1.0 to set up Key Vault</span><span class="sxs-lookup"><span data-stu-id="8505a-113">Use CLI 1.0 to set up Key Vault</span></span>
<span data-ttu-id="8505a-114">To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="8505a-114">To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli.md#create-a-key-vault).</span></span>

<span data-ttu-id="8505a-115">For CLI 1.0, you have to create the key vault before you assign the deployment policy.</span><span class="sxs-lookup"><span data-stu-id="8505a-115">For CLI 1.0, you have to create the key vault before you assign the deployment policy.</span></span> <span data-ttu-id="8505a-116">You can then assign the policy by using the following command:</span><span class="sxs-lookup"><span data-stu-id="8505a-116">You can then assign the policy by using the following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="8505a-117">Use templates to set up Key Vault</span><span class="sxs-lookup"><span data-stu-id="8505a-117">Use templates to set up Key Vault</span></span>
<span data-ttu-id="8505a-118">When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.</span><span class="sxs-lookup"><span data-stu-id="8505a-118">When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.</span></span>

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

<span data-ttu-id="8505a-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="8505a-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>

