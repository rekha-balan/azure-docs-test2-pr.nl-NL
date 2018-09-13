---
title: Set up Key Vault for Windows VMs in Azure Resource Manager | Microsoft Docs
description: How to set up Key Vault for use with an Azure Resource Manager virtual machine.
services: virtual-machines-windows
documentationcenter: ''
author: singhkays
manager: jeconnoc
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
ms.openlocfilehash: e9199d8b743f0bed4feee9f53de9a7cc581d9c03
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44778380"
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a>Set up Key Vault for virtual machines in Azure Resource Manager

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault. To learn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)

> [!NOTE]
> 1. In order for Key Vault to be used with Azure Resource Manager virtual machines, the **EnabledForDeployment** property on Key Vault must be set to true. You can do this in various clients.
> 2. The Key Vault needs to be created in the same subscription and location as the Virtual Machine.
>
>

## <a name="use-powershell-to-set-up-key-vault"></a>Use PowerShell to set up Key Vault
To create a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).

For new key vaults, you can use this PowerShell cmdlet:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

For existing key vaults, you can use this PowerShell cmdlet:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="use-cli-to-set-up-key-vault"></a>Use CLI to set up Key Vault
To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).

For CLI, you have to create the key vault before you assign the deployment policy. You can do this by using the following command:

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-to-set-up-key-vault"></a>Use templates to set up Key Vault
While you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.

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

For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).
