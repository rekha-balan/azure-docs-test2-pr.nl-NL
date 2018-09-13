---
title: Set up Key Vault for Windows VMs in Azure Resource Manager | Microsoft Docs
description: How to set up Key Vault for use with an Azure Resource Manager virtual machine.
services: virtual-machines-windows
documentationcenter: ''
author: singhkays
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 33a483e2-cfbc-4c62-a588-5d9fd52491e2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: kasing
ms.openlocfilehash: e227554e4c80e1d11f90c3a6130d3efe6b00beab
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564425"
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="a8324-103">Set up Key Vault for virtual machines in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a8324-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="a8324-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault.</span><span class="sxs-lookup"><span data-stu-id="a8324-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault.</span></span> <span data-ttu-id="a8324-105">To learn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="a8324-105">To learn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="a8324-106">In order for Key Vault to be used with Azure Resource Manager virtual machines, the **EnabledForDeployment** property on Key Vault must be set to true.</span><span class="sxs-lookup"><span data-stu-id="a8324-106">In order for Key Vault to be used with Azure Resource Manager virtual machines, the **EnabledForDeployment** property on Key Vault must be set to true.</span></span> <span data-ttu-id="a8324-107">You can do this in various clients.</span><span class="sxs-lookup"><span data-stu-id="a8324-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="a8324-108">The Key Vault needs to be created in the same subscription and location as the Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="a8324-108">The Key Vault needs to be created in the same subscription and location as the Virtual Machine.</span></span>
> 
> 

## <a name="use-powershell-to-set-up-key-vault"></a><span data-ttu-id="a8324-109">Use PowerShell to set up Key Vault</span><span class="sxs-lookup"><span data-stu-id="a8324-109">Use PowerShell to set up Key Vault</span></span>
<span data-ttu-id="a8324-110">To create a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span><span class="sxs-lookup"><span data-stu-id="a8324-110">To create a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="a8324-111">For new key vaults, you can use this PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a8324-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="a8324-112">For existing key vaults, you can use this PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a8324-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-to-set-up-key-vault"></a><span data-ttu-id="a8324-113">Us CLI to set up Key Vault</span><span class="sxs-lookup"><span data-stu-id="a8324-113">Us CLI to set up Key Vault</span></span>
<span data-ttu-id="a8324-114">To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli.md#create-a-key-vault).</span><span class="sxs-lookup"><span data-stu-id="a8324-114">To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli.md#create-a-key-vault).</span></span>

<span data-ttu-id="a8324-115">For CLI, you have to create the key vault before you assign the deployment policy.</span><span class="sxs-lookup"><span data-stu-id="a8324-115">For CLI, you have to create the key vault before you assign the deployment policy.</span></span> <span data-ttu-id="a8324-116">You can do this by using the following command:</span><span class="sxs-lookup"><span data-stu-id="a8324-116">You can do this by using the following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="a8324-117">Use templates to set up Key Vault</span><span class="sxs-lookup"><span data-stu-id="a8324-117">Use templates to set up Key Vault</span></span>
<span data-ttu-id="a8324-118">While you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.</span><span class="sxs-lookup"><span data-stu-id="a8324-118">While you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.</span></span>

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

<span data-ttu-id="a8324-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span><span class="sxs-lookup"><span data-stu-id="a8324-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>

