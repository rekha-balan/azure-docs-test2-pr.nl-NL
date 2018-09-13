---
title: Get started with Azure Key Vault | Microsoft Docs
description: Use this tutorial to help you get started with Azure Key Vault to create a hardened container in Azure, to store and manage cryptographic keys and secrets in Azure.
services: key-vault
documentationcenter: ''
author: barclayn
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 36721e1d-38b8-4a15-ba6f-14ed5be4de79
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/10/2018
ms.author: barclayn
ms.openlocfilehash: af4ab892ab84ba2f1a19e72710f23ce5ba1232f9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44785257"
---
# <a name="get-started-with-azure-key-vault"></a><span data-ttu-id="78d08-103">Get started with Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="78d08-103">Get started with Azure Key Vault</span></span>
<span data-ttu-id="78d08-104">This article helps you get started with Azure Key Vault using PowerShell and walks you through the following activities:</span><span class="sxs-lookup"><span data-stu-id="78d08-104">This article helps you get started with Azure Key Vault using PowerShell and walks you through the following activities:</span></span>
- <span data-ttu-id="78d08-105">How to create a hardened container (a vault) in Azure.</span><span class="sxs-lookup"><span data-stu-id="78d08-105">How to create a hardened container (a vault) in Azure.</span></span>
- <span data-ttu-id="78d08-106">How to use KeyVault to store and manage cryptographic keys and secrets in Azure.</span><span class="sxs-lookup"><span data-stu-id="78d08-106">How to use KeyVault to store and manage cryptographic keys and secrets in Azure.</span></span>
- <span data-ttu-id="78d08-107">How an application can use that key or password.</span><span class="sxs-lookup"><span data-stu-id="78d08-107">How an application can use that key or password.</span></span>

<span data-ttu-id="78d08-108">Azure Key Vault is available in most regions.</span><span class="sxs-lookup"><span data-stu-id="78d08-108">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="78d08-109">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="78d08-109">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

<span data-ttu-id="78d08-110">For Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="78d08-110">For Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="78d08-111">Requirements</span><span class="sxs-lookup"><span data-stu-id="78d08-111">Requirements</span></span>
<span data-ttu-id="78d08-112">Before you move forward with the article confirm that you have:</span><span class="sxs-lookup"><span data-stu-id="78d08-112">Before you move forward with the article confirm that you have:</span></span>

- <span data-ttu-id="78d08-113">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="78d08-113">**An Azure subscription**.</span></span> <span data-ttu-id="78d08-114">If you do not have one, you can sign up for a [free account](https://azure.microsoft.com/en-us/free/).</span><span class="sxs-lookup"><span data-stu-id="78d08-114">If you do not have one, you can sign up for a [free account](https://azure.microsoft.com/en-us/free/).</span></span>
- <span data-ttu-id="78d08-115">**Azure PowerShell**, **minimum version of 1.1.0**.</span><span class="sxs-lookup"><span data-stu-id="78d08-115">**Azure PowerShell**, **minimum version of 1.1.0**.</span></span> <span data-ttu-id="78d08-116">To install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="78d08-116">To install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="78d08-117">If you have already installed Azure PowerShell and do not know the version, from the Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span><span class="sxs-lookup"><span data-stu-id="78d08-117">If you have already installed Azure PowerShell and do not know the version, from the Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span> <span data-ttu-id="78d08-118">When you have Azure PowerShell version 0.9.1 through 0.9.8 installed, you can still use this tutorial with some minor changes.</span><span class="sxs-lookup"><span data-stu-id="78d08-118">When you have Azure PowerShell version 0.9.1 through 0.9.8 installed, you can still use this tutorial with some minor changes.</span></span> <span data-ttu-id="78d08-119">For example, you must use the `Switch-AzureMode AzureResourceManager` command and some of the Azure Key Vault commands have changed.</span><span class="sxs-lookup"><span data-stu-id="78d08-119">For example, you must use the `Switch-AzureMode AzureResourceManager` command and some of the Azure Key Vault commands have changed.</span></span> <span data-ttu-id="78d08-120">For a list of the Key Vault cmdlets for versions 0.9.1 through 0.9.8, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span><span class="sxs-lookup"><span data-stu-id="78d08-120">For a list of the Key Vault cmdlets for versions 0.9.1 through 0.9.8, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>
- <span data-ttu-id="78d08-121">**An application that can be configured to use Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="78d08-121">**An application that can be configured to use Key Vault**.</span></span> <span data-ttu-id="78d08-122">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="78d08-122">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="78d08-123">For instructions, see the accompanying **Readme** file.</span><span class="sxs-lookup"><span data-stu-id="78d08-123">For instructions, see the accompanying **Readme** file.</span></span>

>[!NOTE]
<span data-ttu-id="78d08-124">This article assumes a basic understanding of PowerShell and Azure.</span><span class="sxs-lookup"><span data-stu-id="78d08-124">This article assumes a basic understanding of PowerShell and Azure.</span></span> <span data-ttu-id="78d08-125">For more information on PowerShell, see [Getting started with Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx).</span><span class="sxs-lookup"><span data-stu-id="78d08-125">For more information on PowerShell, see [Getting started with Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="78d08-126">To get detailed help for any cmdlet that you see in this tutorial, use the **Get-Help** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="78d08-126">To get detailed help for any cmdlet that you see in this tutorial, use the **Get-Help** cmdlet.</span></span>

```powershell-interactive
Get-Help <cmdlet-name> -Detailed
```
    
<span data-ttu-id="78d08-127">For example, to get help for the **Connect-AzureRmAccount** cmdlet, type:</span><span class="sxs-lookup"><span data-stu-id="78d08-127">For example, to get help for the **Connect-AzureRmAccount** cmdlet, type:</span></span>

```PowerShell
Get-Help Connect-AzureRmAccount -Detailed
```

<span data-ttu-id="78d08-128">You can also read the following articles to get familiar with Azure Resource Manager deployment model in Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="78d08-128">You can also read the following articles to get familiar with Azure Resource Manager deployment model in Azure PowerShell:</span></span>

* [<span data-ttu-id="78d08-129">How to install and configure Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="78d08-129">How to install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="78d08-130">Using Azure PowerShell with Resource Manager</span><span class="sxs-lookup"><span data-stu-id="78d08-130">Using Azure PowerShell with Resource Manager</span></span>](../powershell-azure-resource-manager.md)

## <a id="connect"></a><span data-ttu-id="78d08-131">Connect to your subscriptions</span><span class="sxs-lookup"><span data-stu-id="78d08-131">Connect to your subscriptions</span></span>
<span data-ttu-id="78d08-132">Start an Azure PowerShell session and sign in to your Azure account with the following command:</span><span class="sxs-lookup"><span data-stu-id="78d08-132">Start an Azure PowerShell session and sign in to your Azure account with the following command:</span></span>  

```PowerShell
Connect-AzureRmAccount
```

>[!NOTE]
 <span data-ttu-id="78d08-133">If you are using a specific instance of Azure use the -Environment parameter.</span><span class="sxs-lookup"><span data-stu-id="78d08-133">If you are using a specific instance of Azure use the -Environment parameter.</span></span> <span data-ttu-id="78d08-134">For example:</span><span class="sxs-lookup"><span data-stu-id="78d08-134">For example:</span></span> 
 ```powershell
 Connect-AzureRmAccount –Environment (Get-AzureRmEnvironment –Name AzureUSGovernment)
 ```

<span data-ttu-id="78d08-135">In the pop-up browser window, enter your Azure account user name and password.</span><span class="sxs-lookup"><span data-stu-id="78d08-135">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="78d08-136">Azure PowerShell gets all the subscriptions that are associated with this account and by default, uses the first one.</span><span class="sxs-lookup"><span data-stu-id="78d08-136">Azure PowerShell gets all the subscriptions that are associated with this account and by default, uses the first one.</span></span>

<span data-ttu-id="78d08-137">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span><span class="sxs-lookup"><span data-stu-id="78d08-137">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="78d08-138">Then, to specify the subscription to use, type:</span><span class="sxs-lookup"><span data-stu-id="78d08-138">Then, to specify the subscription to use, type:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscription ID>
```

<span data-ttu-id="78d08-139">For more information about configuring Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="78d08-139">For more information about configuring Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a id="resource"></a><span data-ttu-id="78d08-140">Create a new resource group</span><span class="sxs-lookup"><span data-stu-id="78d08-140">Create a new resource group</span></span>
<span data-ttu-id="78d08-141">When you use Azure Resource Manager, all related resources are created inside a resource group.</span><span class="sxs-lookup"><span data-stu-id="78d08-141">When you use Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="78d08-142">We will create a new resource group named **ContosoResourceGroup** for this tutorial:</span><span class="sxs-lookup"><span data-stu-id="78d08-142">We will create a new resource group named **ContosoResourceGroup** for this tutorial:</span></span>

```powershell
New-AzureRmResourceGroup –Name 'ContosoResourceGroup' –Location 'East US'
```

## <a id="vault"></a><span data-ttu-id="78d08-143">Create a key vault</span><span class="sxs-lookup"><span data-stu-id="78d08-143">Create a key vault</span></span>
<span data-ttu-id="78d08-144">Use the [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) cmdlet to create a key vault.</span><span class="sxs-lookup"><span data-stu-id="78d08-144">Use the [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) cmdlet to create a key vault.</span></span> <span data-ttu-id="78d08-145">This cmdlet has three mandatory parameters: a **resource group name**, a **key vault name**, and the **geographic location**.</span><span class="sxs-lookup"><span data-stu-id="78d08-145">This cmdlet has three mandatory parameters: a **resource group name**, a **key vault name**, and the **geographic location**.</span></span>

<span data-ttu-id="78d08-146">For example, if you use:</span><span class="sxs-lookup"><span data-stu-id="78d08-146">For example, if you use:</span></span>
- <span data-ttu-id="78d08-147">Vault name of **ContosoKeyVault**.</span><span class="sxs-lookup"><span data-stu-id="78d08-147">Vault name of **ContosoKeyVault**.</span></span>
- <span data-ttu-id="78d08-148">Resource group name of **ContosoResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="78d08-148">Resource group name of **ContosoResourceGroup**.</span></span>
- <span data-ttu-id="78d08-149">The location of **East US**.</span><span class="sxs-lookup"><span data-stu-id="78d08-149">The location of **East US**.</span></span>

<span data-ttu-id="78d08-150">you would type:</span><span class="sxs-lookup"><span data-stu-id="78d08-150">you would type:</span></span>

```powershell
New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
```
![Output after Key Vault creation command completes](./media/key-vault-get-started/output-after-creating-keyvault.png)

<span data-ttu-id="78d08-152">The output of this cmdlet shows properties of the key vault that you created.</span><span class="sxs-lookup"><span data-stu-id="78d08-152">The output of this cmdlet shows properties of the key vault that you created.</span></span> <span data-ttu-id="78d08-153">The two most important properties are:</span><span class="sxs-lookup"><span data-stu-id="78d08-153">The two most important properties are:</span></span>

* <span data-ttu-id="78d08-154">**Vault Name**: In the example, this is **ContosoKeyVault**.</span><span class="sxs-lookup"><span data-stu-id="78d08-154">**Vault Name**: In the example, this is **ContosoKeyVault**.</span></span> <span data-ttu-id="78d08-155">You will use this name for other Key Vault cmdlets.</span><span class="sxs-lookup"><span data-stu-id="78d08-155">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="78d08-156">**Vault URI**: In the example, this is https://contosokeyvault.vault.azure.net/.</span><span class="sxs-lookup"><span data-stu-id="78d08-156">**Vault URI**: In the example, this is https://contosokeyvault.vault.azure.net/.</span></span> <span data-ttu-id="78d08-157">Applications that use your vault through its REST API must use this URI.</span><span class="sxs-lookup"><span data-stu-id="78d08-157">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="78d08-158">Your Azure account is now authorized to perform any operations on this key vault.</span><span class="sxs-lookup"><span data-stu-id="78d08-158">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="78d08-159">As yet, nobody else is.</span><span class="sxs-lookup"><span data-stu-id="78d08-159">As yet, nobody else is.</span></span>

> [!NOTE]
> <span data-ttu-id="78d08-160">When you try to create your new key vault you may see the error **The subscription is not registered to use namespace 'Microsoft.KeyVault'**.</span><span class="sxs-lookup"><span data-stu-id="78d08-160">When you try to create your new key vault you may see the error **The subscription is not registered to use namespace 'Microsoft.KeyVault'**.</span></span> <span data-ttu-id="78d08-161">If that message appears run `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"`.</span><span class="sxs-lookup"><span data-stu-id="78d08-161">If that message appears run `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"`.</span></span> <span data-ttu-id="78d08-162">After the registration successfully completes, you can rerun the New-AzureRmKeyVault command.</span><span class="sxs-lookup"><span data-stu-id="78d08-162">After the registration successfully completes, you can rerun the New-AzureRmKeyVault command.</span></span> <span data-ttu-id="78d08-163">For more information, see [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider).</span><span class="sxs-lookup"><span data-stu-id="78d08-163">For more information, see [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider).</span></span>
>
>

## <a id="add"></a><span data-ttu-id="78d08-164">Add a key or secret to the key vault</span><span class="sxs-lookup"><span data-stu-id="78d08-164">Add a key or secret to the key vault</span></span>
<span data-ttu-id="78d08-165">There are a couple of different ways that you may need to interact with Key Vault and keys or secrets.</span><span class="sxs-lookup"><span data-stu-id="78d08-165">There are a couple of different ways that you may need to interact with Key Vault and keys or secrets.</span></span>

### <a name="azure-key-vault-generates-a-software-protected-key"></a><span data-ttu-id="78d08-166">Azure Key Vault generates a software protected key</span><span class="sxs-lookup"><span data-stu-id="78d08-166">Azure Key Vault generates a software protected key</span></span>

<span data-ttu-id="78d08-167">If you want Azure Key Vault to create a software-protected key for you, use the [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) cmdlet, and type:</span><span class="sxs-lookup"><span data-stu-id="78d08-167">If you want Azure Key Vault to create a software-protected key for you, use the [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) cmdlet, and type:</span></span>

```powershell
$key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -Destination 'Software'
```
<span data-ttu-id="78d08-168">to view the URI for this key type:</span><span class="sxs-lookup"><span data-stu-id="78d08-168">to view the URI for this key type:</span></span>
```powershell
$key.id
```

<span data-ttu-id="78d08-169">You can reference a key that you created or uploaded to Azure Key Vault by using its URI.</span><span class="sxs-lookup"><span data-stu-id="78d08-169">You can reference a key that you created or uploaded to Azure Key Vault by using its URI.</span></span> <span data-ttu-id="78d08-170">To get the current version you can use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey**  and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span><span class="sxs-lookup"><span data-stu-id="78d08-170">To get the current version you can use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey**  and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>  

### <a name="importing-an-existing-pfx-file-into-azure-key-vault"></a><span data-ttu-id="78d08-171">Importing an existing PFX file into Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="78d08-171">Importing an existing PFX file into Azure Key Vault</span></span>

<span data-ttu-id="78d08-172">In the case of existing keys stored in a pfx file that you want to upload to Azure Key Vault the steps are different.</span><span class="sxs-lookup"><span data-stu-id="78d08-172">In the case of existing keys stored in a pfx file that you want to upload to Azure Key Vault the steps are different.</span></span> <span data-ttu-id="78d08-173">For example:</span><span class="sxs-lookup"><span data-stu-id="78d08-173">For example:</span></span>
- <span data-ttu-id="78d08-174">If you have an existing software-protected key in a .PFX file</span><span class="sxs-lookup"><span data-stu-id="78d08-174">If you have an existing software-protected key in a .PFX file</span></span>
- <span data-ttu-id="78d08-175">The pfx file is named softkey.pfx</span><span class="sxs-lookup"><span data-stu-id="78d08-175">The pfx file is named softkey.pfx</span></span> 
- <span data-ttu-id="78d08-176">The file is stored in the C drive.</span><span class="sxs-lookup"><span data-stu-id="78d08-176">The file is stored in the C drive.</span></span>

<span data-ttu-id="78d08-177">You can type:</span><span class="sxs-lookup"><span data-stu-id="78d08-177">You can type:</span></span>

```powershell
$securepfxpwd = ConvertTo-SecureString –String '123' –AsPlainText –Force  // This stores the password 123 in the variable $securepfxpwd
```

<span data-ttu-id="78d08-178">Then type the following to import the key from the .PFX file, which protects the key by software in the Key Vault service:</span><span class="sxs-lookup"><span data-stu-id="78d08-178">Then type the following to import the key from the .PFX file, which protects the key by software in the Key Vault service:</span></span>

```powershell
$key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoImportedPFX' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd
```

<span data-ttu-id="78d08-179">To display the URI for this key, type:</span><span class="sxs-lookup"><span data-stu-id="78d08-179">To display the URI for this key, type:</span></span>

```powershell
$Key.id
```
<span data-ttu-id="78d08-180">To view your key, type:</span><span class="sxs-lookup"><span data-stu-id="78d08-180">To view your key, type:</span></span> 

```powershell
Get-AzureKeyVaultKey –VaultName 'ContosoKeyVault'
```
<span data-ttu-id="78d08-181">If you want to view the properties of the PFX file on the portal you would see something similar to the image shown below.</span><span class="sxs-lookup"><span data-stu-id="78d08-181">If you want to view the properties of the PFX file on the portal you would see something similar to the image shown below.</span></span>

![How a certificate looks in the portal](./media/key-vault-get-started/imported-pfx.png)
### <a name="to-add-a-secret-to-azure-key-vault"></a><span data-ttu-id="78d08-183">To add a secret to Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="78d08-183">To add a secret to Azure Key Vault</span></span>

<span data-ttu-id="78d08-184">To add a secret to the vault, which is a password named SQLPassword and has the value of Pa$$w0rd to Azure Key Vault, first convert the value of Pa$$w0rd to a secure string by typing:</span><span class="sxs-lookup"><span data-stu-id="78d08-184">To add a secret to the vault, which is a password named SQLPassword and has the value of Pa$$w0rd to Azure Key Vault, first convert the value of Pa$$w0rd to a secure string by typing:</span></span>

```powershell    
$secretvalue = ConvertTo-SecureString 'Pa$$w0rd' -AsPlainText -Force
```

<span data-ttu-id="78d08-185">Then, type:</span><span class="sxs-lookup"><span data-stu-id="78d08-185">Then, type:</span></span>

```powershell
$secret = Set-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword' -SecretValue $secretvalue
```


<span data-ttu-id="78d08-186">You can now reference this password that you added to Azure Key Vault, by using its URI.</span><span class="sxs-lookup"><span data-stu-id="78d08-186">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="78d08-187">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span><span class="sxs-lookup"><span data-stu-id="78d08-187">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="78d08-188">To display the URI for this secret, type:</span><span class="sxs-lookup"><span data-stu-id="78d08-188">To display the URI for this secret, type:</span></span>

```powershell
$secret.Id
```
<span data-ttu-id="78d08-189">To view your secret, type: `Get-AzureKeyVaultSecret –VaultName 'ContosoKeyVault'` Or alternatively you may view the secret on the portal.</span><span class="sxs-lookup"><span data-stu-id="78d08-189">To view your secret, type: `Get-AzureKeyVaultSecret –VaultName 'ContosoKeyVault'` Or alternatively you may view the secret on the portal.</span></span>

![secret](./media/key-vault-get-started/secret-value.png)

<span data-ttu-id="78d08-191">To view the value contained in the secret as plain text:</span><span class="sxs-lookup"><span data-stu-id="78d08-191">To view the value contained in the secret as plain text:</span></span>
```powershell
(get-azurekeyvaultsecret -vaultName "Contosokeyvault" -name "SQLPassword").SecretValueText
```
<span data-ttu-id="78d08-192">Now, your key vault and key or secret is ready for applications to use.</span><span class="sxs-lookup"><span data-stu-id="78d08-192">Now, your key vault and key or secret is ready for applications to use.</span></span> <span data-ttu-id="78d08-193">You must authorize applications to use them.</span><span class="sxs-lookup"><span data-stu-id="78d08-193">You must authorize applications to use them.</span></span>  

## <a id="register"></a><span data-ttu-id="78d08-194">Register an application with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="78d08-194">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="78d08-195">This step would usually be done by a developer, on a separate computer.</span><span class="sxs-lookup"><span data-stu-id="78d08-195">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="78d08-196">It is not specific to Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="78d08-196">It is not specific to Azure Key Vault.</span></span> <span data-ttu-id="78d08-197">For detailed steps on registering an application with Azure Active Directory you should review the article titled [Integrating applications with Azure Active Directory](../active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad.md) or [Use portal to create an Azure Active Directory application and service principal that can access resources](../azure-resource-manager/resource-group-create-service-principal-portal.md)</span><span class="sxs-lookup"><span data-stu-id="78d08-197">For detailed steps on registering an application with Azure Active Directory you should review the article titled [Integrating applications with Azure Active Directory](../active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad.md) or [Use portal to create an Azure Active Directory application and service principal that can access resources](../azure-resource-manager/resource-group-create-service-principal-portal.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78d08-198">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span><span class="sxs-lookup"><span data-stu-id="78d08-198">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>


<span data-ttu-id="78d08-199">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="78d08-199">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="78d08-200">To do this, the owner of the application must first register the application in their Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="78d08-200">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="78d08-201">At the end of registration, the application owner gets the following values:</span><span class="sxs-lookup"><span data-stu-id="78d08-201">At the end of registration, the application owner gets the following values:</span></span>

- <span data-ttu-id="78d08-202">An **Application ID**</span><span class="sxs-lookup"><span data-stu-id="78d08-202">An **Application ID**</span></span> 
- <span data-ttu-id="78d08-203">An **authentication key** (also known as the shared secret).</span><span class="sxs-lookup"><span data-stu-id="78d08-203">An **authentication key** (also known as the shared secret).</span></span> 

<span data-ttu-id="78d08-204">The application must present both these values to Azure Active Directory, to get a token.</span><span class="sxs-lookup"><span data-stu-id="78d08-204">The application must present both these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="78d08-205">How the application is configured to do this depends on the application.</span><span class="sxs-lookup"><span data-stu-id="78d08-205">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="78d08-206">For the [Key Vault sample application](https://www.microsoft.com/download/details.aspx?id=45343), the application owner sets these values in the app.config file.</span><span class="sxs-lookup"><span data-stu-id="78d08-206">For the [Key Vault sample application](https://www.microsoft.com/download/details.aspx?id=45343), the application owner sets these values in the app.config file.</span></span>


<span data-ttu-id="78d08-207">To register the application in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="78d08-207">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="78d08-208">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78d08-208">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="78d08-209">On the left, click **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="78d08-209">On the left, click **App registrations**.</span></span> <span data-ttu-id="78d08-210">If you don't see app registrations you click on **more services** and find it there.</span><span class="sxs-lookup"><span data-stu-id="78d08-210">If you don't see app registrations you click on **more services** and find it there.</span></span>  
>[!NOTE]
<span data-ttu-id="78d08-211">You must select the same directory that contains the Azure subscription with which you created your key vault.</span><span class="sxs-lookup"><span data-stu-id="78d08-211">You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> 
3. <span data-ttu-id="78d08-212">Click **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="78d08-212">Click **New application registration**.</span></span>
4. <span data-ttu-id="78d08-213">On the **Create** blade provide a name for your application, and then select **WEB APPLICATION AND/OR WEB API** (the default) and specify the **SIGN-ON URL** for your web application.</span><span class="sxs-lookup"><span data-stu-id="78d08-213">On the **Create** blade provide a name for your application, and then select **WEB APPLICATION AND/OR WEB API** (the default) and specify the **SIGN-ON URL** for your web application.</span></span> <span data-ttu-id="78d08-214">If you don't have this information at this time, you can make it up for this step (for example, you could specify http://test1.contoso.com ).</span><span class="sxs-lookup"><span data-stu-id="78d08-214">If you don't have this information at this time, you can make it up for this step (for example, you could specify http://test1.contoso.com ).</span></span> <span data-ttu-id="78d08-215">It does not matter if these sites exist.</span><span class="sxs-lookup"><span data-stu-id="78d08-215">It does not matter if these sites exist.</span></span> 

    ![New application registration](./media/key-vault-get-started/new-application-registration.png)
    >[!WARNING]
    <span data-ttu-id="78d08-217">Make sure that you chose **WEB APPLICATION AND/OR WEB API** if you did not you will not see the **keys** option under settings.</span><span class="sxs-lookup"><span data-stu-id="78d08-217">Make sure that you chose **WEB APPLICATION AND/OR WEB API** if you did not you will not see the **keys** option under settings.</span></span>

5. <span data-ttu-id="78d08-218">Click the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="78d08-218">Click the **Create** button.</span></span>
6. <span data-ttu-id="78d08-219">When the app registration is completed you can see the list of registered apps.</span><span class="sxs-lookup"><span data-stu-id="78d08-219">When the app registration is completed you can see the list of registered apps.</span></span> <span data-ttu-id="78d08-220">Find the app that you just registered and click on it.</span><span class="sxs-lookup"><span data-stu-id="78d08-220">Find the app that you just registered and click on it.</span></span>
7. <span data-ttu-id="78d08-221">Click on the **Registered app** blade copy the **Application ID**</span><span class="sxs-lookup"><span data-stu-id="78d08-221">Click on the **Registered app** blade copy the **Application ID**</span></span>
8. <span data-ttu-id="78d08-222">Click on **All settings**</span><span class="sxs-lookup"><span data-stu-id="78d08-222">Click on **All settings**</span></span>
9. <span data-ttu-id="78d08-223">On the **Settings** blade click on **keys**</span><span class="sxs-lookup"><span data-stu-id="78d08-223">On the **Settings** blade click on **keys**</span></span>
9. <span data-ttu-id="78d08-224">Type in a description in the **Key description** box and select a duration, and then click **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="78d08-224">Type in a description in the **Key description** box and select a duration, and then click **SAVE**.</span></span> <span data-ttu-id="78d08-225">The page refreshes and now shows a key value.</span><span class="sxs-lookup"><span data-stu-id="78d08-225">The page refreshes and now shows a key value.</span></span> 
10. <span data-ttu-id="78d08-226">You will use the **Application ID** and the **Key** information in the next step to set permissions on your vault.</span><span class="sxs-lookup"><span data-stu-id="78d08-226">You will use the **Application ID** and the **Key** information in the next step to set permissions on your vault.</span></span>

## <a id="authorize"></a><span data-ttu-id="78d08-227">Authorize the application to use the key or secret</span><span class="sxs-lookup"><span data-stu-id="78d08-227">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="78d08-228">There are two ways to authorize the application to access the key or secret in the vault.</span><span class="sxs-lookup"><span data-stu-id="78d08-228">There are two ways to authorize the application to access the key or secret in the vault.</span></span>

### <a name="using-powershell"></a><span data-ttu-id="78d08-229">Using PowerShell</span><span class="sxs-lookup"><span data-stu-id="78d08-229">Using PowerShell</span></span>
<span data-ttu-id="78d08-230">To use PowerShell, use the [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="78d08-230">To use PowerShell, use the [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>

<span data-ttu-id="78d08-231">For example, if your vault name is **ContosoKeyVault** and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, run the following:</span><span class="sxs-lookup"><span data-stu-id="78d08-231">For example, if your vault name is **ContosoKeyVault** and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, run the following:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign
```

<span data-ttu-id="78d08-232">If you want to authorize that same application to read secrets in your vault, run the following:</span><span class="sxs-lookup"><span data-stu-id="78d08-232">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get
```
### <a name="using-the-azure-portal"></a><span data-ttu-id="78d08-233">Using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="78d08-233">Using the Azure portal</span></span>
<span data-ttu-id="78d08-234">To change the authorization of an application to use keys or secrets:</span><span class="sxs-lookup"><span data-stu-id="78d08-234">To change the authorization of an application to use keys or secrets:</span></span>
1. <span data-ttu-id="78d08-235">Select **Access Policies** from the Key Vault resource blade</span><span class="sxs-lookup"><span data-stu-id="78d08-235">Select **Access Policies** from the Key Vault resource blade</span></span>
2. <span data-ttu-id="78d08-236">Click the [+ Add new] button at the top of the blade</span><span class="sxs-lookup"><span data-stu-id="78d08-236">Click the [+ Add new] button at the top of the blade</span></span>
3. <span data-ttu-id="78d08-237">Click **Select Principal** to select the application you created earlier</span><span class="sxs-lookup"><span data-stu-id="78d08-237">Click **Select Principal** to select the application you created earlier</span></span>
4. <span data-ttu-id="78d08-238">From the **Key permissions** drop down, select "Decrypt" and "Sign" to authorize the application to decrypt and sign with keys in your vault</span><span class="sxs-lookup"><span data-stu-id="78d08-238">From the **Key permissions** drop down, select "Decrypt" and "Sign" to authorize the application to decrypt and sign with keys in your vault</span></span>
5. <span data-ttu-id="78d08-239">From the **Secret permissions** drop-down, select "Get" to allow the application to read secrets in the vault</span><span class="sxs-lookup"><span data-stu-id="78d08-239">From the **Secret permissions** drop-down, select "Get" to allow the application to read secrets in the vault</span></span>

## <a id="HSM"></a><span data-ttu-id="78d08-240">Working with a hardware security module (HSM)</span><span class="sxs-lookup"><span data-stu-id="78d08-240">Working with a hardware security module (HSM)</span></span>
<span data-ttu-id="78d08-241">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span><span class="sxs-lookup"><span data-stu-id="78d08-241">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="78d08-242">The HSMs are FIPS 140-2 Level 2 validated.</span><span class="sxs-lookup"><span data-stu-id="78d08-242">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="78d08-243">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete).</span><span class="sxs-lookup"><span data-stu-id="78d08-243">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete).</span></span>

<span data-ttu-id="78d08-244">To create these HSM-protected keys, you must use the [Azure Key Vault Premium service tier to support HSM-protected keys](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="78d08-244">To create these HSM-protected keys, you must use the [Azure Key Vault Premium service tier to support HSM-protected keys](https://azure.microsoft.com/pricing/details/key-vault/).</span></span> <span data-ttu-id="78d08-245">In addition, note that this functionality is not available for Azure China.</span><span class="sxs-lookup"><span data-stu-id="78d08-245">In addition, note that this functionality is not available for Azure China.</span></span>

<span data-ttu-id="78d08-246">When you create the key vault, add the **-SKU** parameter:</span><span class="sxs-lookup"><span data-stu-id="78d08-246">When you create the key vault, add the **-SKU** parameter:</span></span>

```powershell
New-AzureRmKeyVault -VaultName 'ContosoKeyVaultHSM' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US' -SKU 'Premium'
```


<span data-ttu-id="78d08-247">You can add software-protected keys (as shown earlier) and HSM-protected keys to this key vault.</span><span class="sxs-lookup"><span data-stu-id="78d08-247">You can add software-protected keys (as shown earlier) and HSM-protected keys to this key vault.</span></span> <span data-ttu-id="78d08-248">To create an HSM-protected key, set the **-Destination** parameter to 'HSM':</span><span class="sxs-lookup"><span data-stu-id="78d08-248">To create an HSM-protected key, set the **-Destination** parameter to 'HSM':</span></span>

```powershell
$key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -Destination 'HSM'
```

<span data-ttu-id="78d08-249">You can use the following command to import a key from a .PFX file on your computer.</span><span class="sxs-lookup"><span data-stu-id="78d08-249">You can use the following command to import a key from a .PFX file on your computer.</span></span> <span data-ttu-id="78d08-250">This command imports the key into HSMs in the Key Vault service:</span><span class="sxs-lookup"><span data-stu-id="78d08-250">This command imports the key into HSMs in the Key Vault service:</span></span>

```powershell
$key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd -Destination 'HSM'
```

<span data-ttu-id="78d08-251">The next command imports a “bring your own key" (BYOK) package.</span><span class="sxs-lookup"><span data-stu-id="78d08-251">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="78d08-252">This scenario lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span><span class="sxs-lookup"><span data-stu-id="78d08-252">This scenario lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

```powershell
$key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\ITByok.byok' -Destination 'HSM'
```

<span data-ttu-id="78d08-253">For more detailed instructions about how to generate this BYOK package, see [How to generate and transfer HSM-protected keys for Azure Key Vault](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="78d08-253">For more detailed instructions about how to generate this BYOK package, see [How to generate and transfer HSM-protected keys for Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a id="delete"></a><span data-ttu-id="78d08-254">Delete the key vault and associated keys and secrets</span><span class="sxs-lookup"><span data-stu-id="78d08-254">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="78d08-255">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the [Remove-AzureRmKeyVault](/powershell/module/azurerm.keyvault/remove-azurermkeyvault) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="78d08-255">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the [Remove-AzureRmKeyVault](/powershell/module/azurerm.keyvault/remove-azurermkeyvault) cmdlet:</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoKeyVault'
```

<span data-ttu-id="78d08-256">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span><span class="sxs-lookup"><span data-stu-id="78d08-256">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName 'ContosoResourceGroup'
```

## <a id="other"></a><span data-ttu-id="78d08-257">Other Azure PowerShell Cmdlets</span><span class="sxs-lookup"><span data-stu-id="78d08-257">Other Azure PowerShell Cmdlets</span></span>
<span data-ttu-id="78d08-258">Other commands that you might find useful for managing Azure Key Vault:</span><span class="sxs-lookup"><span data-stu-id="78d08-258">Other commands that you might find useful for managing Azure Key Vault:</span></span>

- <span data-ttu-id="78d08-259">`$Keys = Get-AzureKeyVaultKey -VaultName 'ContosoKeyVault'`: This command gets a tabular display of all keys and selected properties.</span><span class="sxs-lookup"><span data-stu-id="78d08-259">`$Keys = Get-AzureKeyVaultKey -VaultName 'ContosoKeyVault'`: This command gets a tabular display of all keys and selected properties.</span></span>
- <span data-ttu-id="78d08-260">`$Keys[0]`: This command displays a full list of properties for the specified key</span><span class="sxs-lookup"><span data-stu-id="78d08-260">`$Keys[0]`: This command displays a full list of properties for the specified key</span></span>
- <span data-ttu-id="78d08-261">`Get-AzureKeyVaultSecret`: This command lists a tabular display of all secret names and selected properties.</span><span class="sxs-lookup"><span data-stu-id="78d08-261">`Get-AzureKeyVaultSecret`: This command lists a tabular display of all secret names and selected properties.</span></span>
- <span data-ttu-id="78d08-262">`Remove-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey'`: Example how to remove a specific key.</span><span class="sxs-lookup"><span data-stu-id="78d08-262">`Remove-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey'`: Example how to remove a specific key.</span></span>
- <span data-ttu-id="78d08-263">`Remove-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword'`: Example how to remove a specific secret.</span><span class="sxs-lookup"><span data-stu-id="78d08-263">`Remove-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword'`: Example how to remove a specific secret.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78d08-264">Next steps</span><span class="sxs-lookup"><span data-stu-id="78d08-264">Next steps</span></span>

- <span data-ttu-id="78d08-265">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="78d08-265">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>
- <span data-ttu-id="78d08-266">To see how your key vault is being used, see [Azure Key Vault Logging](key-vault-logging.md).</span><span class="sxs-lookup"><span data-stu-id="78d08-266">To see how your key vault is being used, see [Azure Key Vault Logging](key-vault-logging.md).</span></span>
- <span data-ttu-id="78d08-267">For a follow-up tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span><span class="sxs-lookup"><span data-stu-id="78d08-267">For a follow-up tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>
- <span data-ttu-id="78d08-268">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="78d08-268">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
- <span data-ttu-id="78d08-269">For a list of the latest Azure PowerShell cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span><span class="sxs-lookup"><span data-stu-id="78d08-269">For a list of the latest Azure PowerShell cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>
