---
title: Azure Quickstart - Set & retrieve a secret from Key Vault using PowerShell | Microsoft Docs
description: ''
services: key-vault
author: barclayn
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 1126f665-2e6c-4cca-897e-7d61842e8334
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.custom: mvc
ms.date: 08/28/2018
ms.author: barclayn
ms.openlocfilehash: f3ea500c8e48f4a509782657ad2fe750bf3a7ed6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856663"
---
# <a name="quickstart-set-and-retrieve-a-secret-from-azure-key-vault-using-powershell"></a><span data-ttu-id="cfdf1-102">Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell</span><span class="sxs-lookup"><span data-stu-id="cfdf1-102">Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell</span></span>

<span data-ttu-id="cfdf1-103">Azure Key Vault is a cloud service that works as a secure secrets store.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-103">Azure Key Vault is a cloud service that works as a secure secrets store.</span></span> <span data-ttu-id="cfdf1-104">You can securely store keys, passwords, certificates, and other secrets.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-104">You can securely store keys, passwords, certificates, and other secrets.</span></span> <span data-ttu-id="cfdf1-105">For more information on Key Vault, you may review the [Overview](key-vault-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cfdf1-105">For more information on Key Vault, you may review the [Overview](key-vault-overview.md).</span></span> <span data-ttu-id="cfdf1-106">In this quickstart, you use PowerShell to create a key vault.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-106">In this quickstart, you use PowerShell to create a key vault.</span></span> <span data-ttu-id="cfdf1-107">You then store a secret in the newly created vault.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-107">You then store a secret in the newly created vault.</span></span>

<span data-ttu-id="cfdf1-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="cfdf1-109">If you choose to install and use PowerShell locally, this tutorial requires Azure PowerShell module version 5.1.1 or later.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-109">If you choose to install and use PowerShell locally, this tutorial requires Azure PowerShell module version 5.1.1 or later.</span></span> <span data-ttu-id="cfdf1-110">Run `Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-110">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="cfdf1-111">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="cfdf1-111">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="cfdf1-112">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-112">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

```azurepowershell-interactive
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="cfdf1-113">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="cfdf1-113">Create a resource group</span></span>

<span data-ttu-id="cfdf1-114">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="cfdf1-114">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="cfdf1-115">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```azurepowershell-interactive
New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS
```

## <a name="create-a-key-vault"></a><span data-ttu-id="cfdf1-116">Create a Key Vault</span><span class="sxs-lookup"><span data-stu-id="cfdf1-116">Create a Key Vault</span></span>

<span data-ttu-id="cfdf1-117">Next you create a Key Vault.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-117">Next you create a Key Vault.</span></span> <span data-ttu-id="cfdf1-118">When doing this step, you need some information:</span><span class="sxs-lookup"><span data-stu-id="cfdf1-118">When doing this step, you need some information:</span></span>

<span data-ttu-id="cfdf1-119">Although we use “Contoso KeyVault2” as the name for our Key Vault throughout this quickstart, you must use a unique name.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-119">Although we use “Contoso KeyVault2” as the name for our Key Vault throughout this quickstart, you must use a unique name.</span></span>

- <span data-ttu-id="cfdf1-120">**Vault name** Contoso-Vault2.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-120">**Vault name** Contoso-Vault2.</span></span>
- <span data-ttu-id="cfdf1-121">**Resource group name** ContosoResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-121">**Resource group name** ContosoResourceGroup.</span></span>
- <span data-ttu-id="cfdf1-122">**Location** East US.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-122">**Location** East US.</span></span>

```azurepowershell-interactive
New-AzureRmKeyVault -VaultName 'Contoso-Vault2' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
```

<span data-ttu-id="cfdf1-123">The output of this cmdlet shows properties of the newly created key vault.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-123">The output of this cmdlet shows properties of the newly created key vault.</span></span> <span data-ttu-id="cfdf1-124">Take note of the two properties listed below:</span><span class="sxs-lookup"><span data-stu-id="cfdf1-124">Take note of the two properties listed below:</span></span>

* <span data-ttu-id="cfdf1-125">**Vault Name**: In the example that is **Contoso-Vault2**.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-125">**Vault Name**: In the example that is **Contoso-Vault2**.</span></span> <span data-ttu-id="cfdf1-126">You will use this name for other Key Vault cmdlets.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-126">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="cfdf1-127">**Vault URI**: In this example that is https://contosokeyvault.vault.azure.net/.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-127">**Vault URI**: In this example that is https://contosokeyvault.vault.azure.net/.</span></span> <span data-ttu-id="cfdf1-128">Applications that use your vault through its REST API must use this URI.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-128">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="cfdf1-129">After vault creation your Azure account is the only account allowed to do anything on this new vault.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-129">After vault creation your Azure account is the only account allowed to do anything on this new vault.</span></span>

![Output after Key Vault creation command completes](./media/quick-create-powershell/output-after-creating-keyvault.png)

## <a name="adding-a-secret-to-key-vault"></a><span data-ttu-id="cfdf1-131">Adding a secret to Key Vault</span><span class="sxs-lookup"><span data-stu-id="cfdf1-131">Adding a secret to Key Vault</span></span>

<span data-ttu-id="cfdf1-132">To add a secret to the vault, you just need to take a couple of steps.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-132">To add a secret to the vault, you just need to take a couple of steps.</span></span> <span data-ttu-id="cfdf1-133">In this case, you add a password that could be used by an application.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-133">In this case, you add a password that could be used by an application.</span></span> <span data-ttu-id="cfdf1-134">The password is called **ExamplePassword** and stores the value of '''**Pa$$w0rd**''' in it.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-134">The password is called **ExamplePassword** and stores the value of '''**Pa$$w0rd**''' in it.</span></span>

<span data-ttu-id="cfdf1-135">First convert the value of Pa$$w0rd to a secure string by typing:</span><span class="sxs-lookup"><span data-stu-id="cfdf1-135">First convert the value of Pa$$w0rd to a secure string by typing:</span></span>

```azurepowershell-interactive
$secretvalue = ConvertTo-SecureString 'Pa$$w0rd' -AsPlainText -Force
```

<span data-ttu-id="cfdf1-136">Then, type the PowerShell commands below to create a secret in Key Vault called **ExamplePassword** with the value **Pa$$w0rd** :</span><span class="sxs-lookup"><span data-stu-id="cfdf1-136">Then, type the PowerShell commands below to create a secret in Key Vault called **ExamplePassword** with the value **Pa$$w0rd** :</span></span>

```azurepowershell-interactive
$secret = Set-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'ExamplePassword' -SecretValue $secretvalue
```

<span data-ttu-id="cfdf1-137">To view the value contained in the secret as plain text:</span><span class="sxs-lookup"><span data-stu-id="cfdf1-137">To view the value contained in the secret as plain text:</span></span>

```azurepowershell-interactive
(Get-AzureKeyVaultSecret -vaultName "Contosokeyvault" -name "ExamplePassword").SecretValueText
```

<span data-ttu-id="cfdf1-138">Now, you have created a Key Vault, stored a secret, and retrieved it.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-138">Now, you have created a Key Vault, stored a secret, and retrieved it.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="cfdf1-139">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="cfdf1-139">Clean up resources</span></span>

 <span data-ttu-id="cfdf1-140">Other quickstarts and tutorials in this collection build upon this quickstart.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-140">Other quickstarts and tutorials in this collection build upon this quickstart.</span></span> <span data-ttu-id="cfdf1-141">If you plan to continue on to work with other quickstarts and tutorials, you may want to leave these resources in place.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-141">If you plan to continue on to work with other quickstarts and tutorials, you may want to leave these resources in place.</span></span>

<span data-ttu-id="cfdf1-142">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, Key Vault, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-142">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, Key Vault, and all related resources.</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name ContosoResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="cfdf1-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="cfdf1-143">Next steps</span></span>

<span data-ttu-id="cfdf1-144">In this quickstart, you have created a Key Vault and stored a software key in it.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-144">In this quickstart, you have created a Key Vault and stored a software key in it.</span></span> <span data-ttu-id="cfdf1-145">To learn more about Key Vault and how you can use it with your applications continue to the tutorial for web applications working with Key Vault.</span><span class="sxs-lookup"><span data-stu-id="cfdf1-145">To learn more about Key Vault and how you can use it with your applications continue to the tutorial for web applications working with Key Vault.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="cfdf1-146">To learn how to read a secret from Key Vault from a web application using managed identities for Azure resources, continue with the following tutorial [Configure an Azure web application to read a secret from Key vault](quick-create-net.md).</span><span class="sxs-lookup"><span data-stu-id="cfdf1-146">To learn how to read a secret from Key Vault from a web application using managed identities for Azure resources, continue with the following tutorial [Configure an Azure web application to read a secret from Key vault](quick-create-net.md).</span></span>
