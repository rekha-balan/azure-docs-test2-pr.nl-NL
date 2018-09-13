---
title: Get started with Azure Key Vault | Microsoft Docs
description: Use this tutorial to help you get started with Azure Key Vault to create a hardened container in Azure, to store and manage cryptographic keys and secrets in Azure.
services: key-vault
documentationcenter: ''
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 36721e1d-38b8-4a15-ba6f-14ed5be4de79
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 10/24/2016
ms.author: cabailey
ms.openlocfilehash: 115a718977906b3e647b628017f7ab46a588d7f2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670602"
---
# <a name="get-started-with-azure-key-vault"></a><span data-ttu-id="f2a03-103">Get started with Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f2a03-103">Get started with Azure Key Vault</span></span>
<span data-ttu-id="f2a03-104">Azure Key Vault is available in most regions.</span><span class="sxs-lookup"><span data-stu-id="f2a03-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="f2a03-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="f2a03-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="f2a03-106">Introduction</span><span class="sxs-lookup"><span data-stu-id="f2a03-106">Introduction</span></span>
<span data-ttu-id="f2a03-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span><span class="sxs-lookup"><span data-stu-id="f2a03-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="f2a03-108">It walks you through the process of using Azure PowerShell to create a vault that contains a key or password that you can then use with an Azure application.</span><span class="sxs-lookup"><span data-stu-id="f2a03-108">It walks you through the process of using Azure PowerShell to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="f2a03-109">It then shows you how an application can use that key or password.</span><span class="sxs-lookup"><span data-stu-id="f2a03-109">It then shows you how an application can use that key or password.</span></span>

<span data-ttu-id="f2a03-110">**Estimated time to complete:** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="f2a03-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="f2a03-111">This tutorial does not include instructions for how to write the Azure application that one of the steps includes, namely how to authorize an application to use a key or secret in the key vault.</span><span class="sxs-lookup"><span data-stu-id="f2a03-111">This tutorial does not include instructions for how to write the Azure application that one of the steps includes, namely how to authorize an application to use a key or secret in the key vault.</span></span>
> 
> <span data-ttu-id="f2a03-112">This tutorial uses Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2a03-112">This tutorial uses Azure PowerShell.</span></span> <span data-ttu-id="f2a03-113">For Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f2a03-113">For Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli.md).</span></span>
> 
> 

<span data-ttu-id="f2a03-114">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="f2a03-114">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2a03-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f2a03-115">Prerequisites</span></span>
<span data-ttu-id="f2a03-116">To complete this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="f2a03-116">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="f2a03-117">A subscription to Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f2a03-117">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="f2a03-118">If you do not have one, you can sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f2a03-118">If you do not have one, you can sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f2a03-119">Azure PowerShell, **minimum version of 1.1.0**.</span><span class="sxs-lookup"><span data-stu-id="f2a03-119">Azure PowerShell, **minimum version of 1.1.0**.</span></span> <span data-ttu-id="f2a03-120">To install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="f2a03-120">To install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="f2a03-121">If you have already installed Azure PowerShell and do not know the version, from the Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span><span class="sxs-lookup"><span data-stu-id="f2a03-121">If you have already installed Azure PowerShell and do not know the version, from the Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span> <span data-ttu-id="f2a03-122">When you have Azure PowerShell version 0.9.1 through 0.9.8 installed, you can still use this tutorial with some minor changes.</span><span class="sxs-lookup"><span data-stu-id="f2a03-122">When you have Azure PowerShell version 0.9.1 through 0.9.8 installed, you can still use this tutorial with some minor changes.</span></span> <span data-ttu-id="f2a03-123">For example, you must use the `Switch-AzureMode AzureResourceManager` command and some of the Azure Key Vault commands have changed.</span><span class="sxs-lookup"><span data-stu-id="f2a03-123">For example, you must use the `Switch-AzureMode AzureResourceManager` command and some of the Azure Key Vault commands have changed.</span></span> <span data-ttu-id="f2a03-124">For a list of the Key Vault cmdlets for versions 0.9.1 through 0.9.8, see [Azure Key Vault Cmdlets](https://msdn.microsoft.com/library/azure/dn868052\(v=azure.98\).aspx).</span><span class="sxs-lookup"><span data-stu-id="f2a03-124">For a list of the Key Vault cmdlets for versions 0.9.1 through 0.9.8, see [Azure Key Vault Cmdlets](https://msdn.microsoft.com/library/azure/dn868052\(v=azure.98\).aspx).</span></span> 
* <span data-ttu-id="f2a03-125">An application that will be configured to use the key or password that you create in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f2a03-125">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="f2a03-126">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/en-us/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="f2a03-126">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/en-us/download/details.aspx?id=45343).</span></span> <span data-ttu-id="f2a03-127">For instructions, see the accompanying Readme file.</span><span class="sxs-lookup"><span data-stu-id="f2a03-127">For instructions, see the accompanying Readme file.</span></span>

<span data-ttu-id="f2a03-128">This tutorial is designed for Azure PowerShell beginners, but it assumes that you understand the basic concepts, such as modules, cmdlets, and sessions.</span><span class="sxs-lookup"><span data-stu-id="f2a03-128">This tutorial is designed for Azure PowerShell beginners, but it assumes that you understand the basic concepts, such as modules, cmdlets, and sessions.</span></span> <span data-ttu-id="f2a03-129">For more information, see [Getting started with Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2a03-129">For more information, see [Getting started with Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx).</span></span>

<span data-ttu-id="f2a03-130">To get detailed help for any cmdlet that you see in this tutorial, use the **Get-Help** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f2a03-130">To get detailed help for any cmdlet that you see in this tutorial, use the **Get-Help** cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="f2a03-131">For example, to get help for the **Login-AzureRmAccount** cmdlet, type:</span><span class="sxs-lookup"><span data-stu-id="f2a03-131">For example, to get help for the **Login-AzureRmAccount** cmdlet, type:</span></span>

    Get-Help Login-AzureRmAccount -Detailed

<span data-ttu-id="f2a03-132">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f2a03-132">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure PowerShell:</span></span>

* [<span data-ttu-id="f2a03-133">How to install and configure Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2a03-133">How to install and configure Azure PowerShell</span></span>](/powershell/azureps-cmdlets-docs)
* [<span data-ttu-id="f2a03-134">Using Azure PowerShell with Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f2a03-134">Using Azure PowerShell with Resource Manager</span></span>](../powershell-azure-resource-manager.md)

## <a id="connect"></a><span data-ttu-id="f2a03-135">Connect to your subscriptions</span><span class="sxs-lookup"><span data-stu-id="f2a03-135">Connect to your subscriptions</span></span>
<span data-ttu-id="f2a03-136">Start an Azure PowerShell session and sign in to your Azure account with the following command:</span><span class="sxs-lookup"><span data-stu-id="f2a03-136">Start an Azure PowerShell session and sign in to your Azure account with the following command:</span></span>  

    Login-AzureRmAccount 

<span data-ttu-id="f2a03-137">Note that if you are using a specific instance of Azure, for example, Azure Government, use the -Environment parameter with this command.</span><span class="sxs-lookup"><span data-stu-id="f2a03-137">Note that if you are using a specific instance of Azure, for example, Azure Government, use the -Environment parameter with this command.</span></span> <span data-ttu-id="f2a03-138">For example: `Login-AzureRmAccount –Environment (Get-AzureRmEnvironment –Name AzureUSGovernment)`</span><span class="sxs-lookup"><span data-stu-id="f2a03-138">For example: `Login-AzureRmAccount –Environment (Get-AzureRmEnvironment –Name AzureUSGovernment)`</span></span>

<span data-ttu-id="f2a03-139">In the pop-up browser window, enter your Azure account user name and password.</span><span class="sxs-lookup"><span data-stu-id="f2a03-139">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="f2a03-140">Azure PowerShell gets all the subscriptions that are associated with this account and by default, uses the first one.</span><span class="sxs-lookup"><span data-stu-id="f2a03-140">Azure PowerShell gets all the subscriptions that are associated with this account and by default, uses the first one.</span></span>

<span data-ttu-id="f2a03-141">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span><span class="sxs-lookup"><span data-stu-id="f2a03-141">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="f2a03-142">Then, to specify the subscription to use, type:</span><span class="sxs-lookup"><span data-stu-id="f2a03-142">Then, to specify the subscription to use, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

<span data-ttu-id="f2a03-143">For more information about configuring Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="f2a03-143">For more information about configuring Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

## <a id="resource"></a><span data-ttu-id="f2a03-144">Create a new resource group</span><span class="sxs-lookup"><span data-stu-id="f2a03-144">Create a new resource group</span></span>
<span data-ttu-id="f2a03-145">When you use Azure Resource Manager, all related resources are created inside a resource group.</span><span class="sxs-lookup"><span data-stu-id="f2a03-145">When you use Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="f2a03-146">We will create a new resource group named **ContosoResourceGroup** for this tutorial:</span><span class="sxs-lookup"><span data-stu-id="f2a03-146">We will create a new resource group named **ContosoResourceGroup** for this tutorial:</span></span>

    New-AzureRmResourceGroup –Name 'ContosoResourceGroup' –Location 'East Asia'


## <a id="vault"></a><span data-ttu-id="f2a03-147">Create a key vault</span><span class="sxs-lookup"><span data-stu-id="f2a03-147">Create a key vault</span></span>
<span data-ttu-id="f2a03-148">Use the [New-AzureRmKeyVault](https://msdn.microsoft.com/library/azure/mt603736\(v=azure.300\).aspx) cmdlet to create a key vault.</span><span class="sxs-lookup"><span data-stu-id="f2a03-148">Use the [New-AzureRmKeyVault](https://msdn.microsoft.com/library/azure/mt603736\(v=azure.300\).aspx) cmdlet to create a key vault.</span></span> <span data-ttu-id="f2a03-149">This cmdlet has three mandatory parameters: a **resource group name**, a **key vault name**, and the **geographic location**.</span><span class="sxs-lookup"><span data-stu-id="f2a03-149">This cmdlet has three mandatory parameters: a **resource group name**, a **key vault name**, and the **geographic location**.</span></span>

<span data-ttu-id="f2a03-150">For example, if you use the vault name of **ContosoKeyVault**, the resource group name of **ContosoResourceGroup**, and the location of **East Asia**, type:</span><span class="sxs-lookup"><span data-stu-id="f2a03-150">For example, if you use the vault name of **ContosoKeyVault**, the resource group name of **ContosoResourceGroup**, and the location of **East Asia**, type:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

<span data-ttu-id="f2a03-151">The output of this cmdlet shows properties of the key vault that you’ve just created.</span><span class="sxs-lookup"><span data-stu-id="f2a03-151">The output of this cmdlet shows properties of the key vault that you’ve just created.</span></span> <span data-ttu-id="f2a03-152">The two most important properties are:</span><span class="sxs-lookup"><span data-stu-id="f2a03-152">The two most important properties are:</span></span>

* <span data-ttu-id="f2a03-153">**Vault Name**: In the example, this is **ContosoKeyVault**.</span><span class="sxs-lookup"><span data-stu-id="f2a03-153">**Vault Name**: In the example, this is **ContosoKeyVault**.</span></span> <span data-ttu-id="f2a03-154">You will use this name for other Key Vault cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f2a03-154">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="f2a03-155">**Vault URI**: In the example, this is https://contosokeyvault.vault.azure.net/.</span><span class="sxs-lookup"><span data-stu-id="f2a03-155">**Vault URI**: In the example, this is https://contosokeyvault.vault.azure.net/.</span></span> <span data-ttu-id="f2a03-156">Applications that use your vault through its REST API must use this URI.</span><span class="sxs-lookup"><span data-stu-id="f2a03-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="f2a03-157">Your Azure account is now authorized to perform any operations on this key vault.</span><span class="sxs-lookup"><span data-stu-id="f2a03-157">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="f2a03-158">As yet, nobody else is.</span><span class="sxs-lookup"><span data-stu-id="f2a03-158">As yet, nobody else is.</span></span>

> [!NOTE]
> <span data-ttu-id="f2a03-159">If you see the error **The subscription is not registered to use namespace 'Microsoft.KeyVault'** when you try to create your new key vault, run `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"` and then rerun your New-AzureRmKeyVault command.</span><span class="sxs-lookup"><span data-stu-id="f2a03-159">If you see the error **The subscription is not registered to use namespace 'Microsoft.KeyVault'** when you try to create your new key vault, run `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"` and then rerun your New-AzureRmKeyVault command.</span></span> <span data-ttu-id="f2a03-160">For more information, see [Register-AzureRmResourceProvider](https://msdn.microsoft.com/library/azure/mt759831\(v=azure.300\).aspx).</span><span class="sxs-lookup"><span data-stu-id="f2a03-160">For more information, see [Register-AzureRmResourceProvider](https://msdn.microsoft.com/library/azure/mt759831\(v=azure.300\).aspx).</span></span>
> 
> 

## <a id="add"></a><span data-ttu-id="f2a03-161">Add a key or secret to the key vault</span><span class="sxs-lookup"><span data-stu-id="f2a03-161">Add a key or secret to the key vault</span></span>
<span data-ttu-id="f2a03-162">If you want Azure Key Vault to create a software-protected key for you, use the [Add-AzureKeyVaultKey](https://msdn.microsoft.com/library/azure/dn868048\(v=azure.300\).aspx) cmdlet, and type the following:</span><span class="sxs-lookup"><span data-stu-id="f2a03-162">If you want Azure Key Vault to create a software-protected key for you, use the [Add-AzureKeyVaultKey](https://msdn.microsoft.com/library/azure/dn868048\(v=azure.300\).aspx) cmdlet, and type the following:</span></span>

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -Destination 'Software'

<span data-ttu-id="f2a03-163">However, if you have an existing software-protected key in a .PFX file saved to your C:\ drive in a file named softkey.pfx that you want to upload to Azure Key Vault, type the following to set the variable **securepfxpwd** for a password of **123** for the .PFX file:</span><span class="sxs-lookup"><span data-stu-id="f2a03-163">However, if you have an existing software-protected key in a .PFX file saved to your C:\ drive in a file named softkey.pfx that you want to upload to Azure Key Vault, type the following to set the variable **securepfxpwd** for a password of **123** for the .PFX file:</span></span>

    $securepfxpwd = ConvertTo-SecureString –String '123' –AsPlainText –Force

<span data-ttu-id="f2a03-164">Then type the following to import the key from the .PFX file, which protects the key by software in the Key Vault service:</span><span class="sxs-lookup"><span data-stu-id="f2a03-164">Then type the following to import the key from the .PFX file, which protects the key by software in the Key Vault service:</span></span>

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd


<span data-ttu-id="f2a03-165">You can now reference this key that you created or uploaded to Azure Key Vault, by using its URI.</span><span class="sxs-lookup"><span data-stu-id="f2a03-165">You can now reference this key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="f2a03-166">Use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span><span class="sxs-lookup"><span data-stu-id="f2a03-166">Use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>  

<span data-ttu-id="f2a03-167">To display the URI for this key, type:</span><span class="sxs-lookup"><span data-stu-id="f2a03-167">To display the URI for this key, type:</span></span>

    $Key.key.kid

<span data-ttu-id="f2a03-168">To add a secret to the vault, which is a password named SQLPassword and has the value of Pa$$w0rd to Azure Key Vault, first convert the value of Pa$$w0rd to a secure string by typing the following:</span><span class="sxs-lookup"><span data-stu-id="f2a03-168">To add a secret to the vault, which is a password named SQLPassword and has the value of Pa$$w0rd to Azure Key Vault, first convert the value of Pa$$w0rd to a secure string by typing the following:</span></span>

    $secretvalue = ConvertTo-SecureString 'Pa$$w0rd' -AsPlainText -Force

<span data-ttu-id="f2a03-169">Then, type the following:</span><span class="sxs-lookup"><span data-stu-id="f2a03-169">Then, type the following:</span></span>

    $secret = Set-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword' -SecretValue $secretvalue

<span data-ttu-id="f2a03-170">You can now reference this password that you added to Azure Key Vault, by using its URI.</span><span class="sxs-lookup"><span data-stu-id="f2a03-170">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="f2a03-171">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span><span class="sxs-lookup"><span data-stu-id="f2a03-171">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="f2a03-172">To display the URI for this secret, type:</span><span class="sxs-lookup"><span data-stu-id="f2a03-172">To display the URI for this secret, type:</span></span>

    $secret.Id

<span data-ttu-id="f2a03-173">Let’s view the key or secret that you just created:</span><span class="sxs-lookup"><span data-stu-id="f2a03-173">Let’s view the key or secret that you just created:</span></span>

* <span data-ttu-id="f2a03-174">To view your key, type: `Get-AzureKeyVaultKey –VaultName 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="f2a03-174">To view your key, type: `Get-AzureKeyVaultKey –VaultName 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="f2a03-175">To view your secret, type: `Get-AzureKeyVaultSecret –VaultName 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="f2a03-175">To view your secret, type: `Get-AzureKeyVaultSecret –VaultName 'ContosoKeyVault'`</span></span>

<span data-ttu-id="f2a03-176">Now, your key vault and key or secret is ready for applications to use.</span><span class="sxs-lookup"><span data-stu-id="f2a03-176">Now, your key vault and key or secret is ready for applications to use.</span></span> <span data-ttu-id="f2a03-177">You must authorize applications to use them.</span><span class="sxs-lookup"><span data-stu-id="f2a03-177">You must authorize applications to use them.</span></span>  

## <a id="register"></a><span data-ttu-id="f2a03-178">Register an application with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f2a03-178">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="f2a03-179">This step would usually be done by a developer, on a separate computer.</span><span class="sxs-lookup"><span data-stu-id="f2a03-179">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="f2a03-180">It is not specific to Azure Key Vault, but is included here for completeness.</span><span class="sxs-lookup"><span data-stu-id="f2a03-180">It is not specific to Azure Key Vault, but is included here for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2a03-181">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span><span class="sxs-lookup"><span data-stu-id="f2a03-181">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
> 
> 

<span data-ttu-id="f2a03-182">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f2a03-182">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="f2a03-183">To do this, the owner of the application must first register the application in their Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f2a03-183">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="f2a03-184">At the end of registration, the application owner gets the following values:</span><span class="sxs-lookup"><span data-stu-id="f2a03-184">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="f2a03-185">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span><span class="sxs-lookup"><span data-stu-id="f2a03-185">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="f2a03-186">The application must present both these values to Azure Active Directory, to get a token.</span><span class="sxs-lookup"><span data-stu-id="f2a03-186">The application must present both these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="f2a03-187">How the application is configured to do this depends on the application.</span><span class="sxs-lookup"><span data-stu-id="f2a03-187">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="f2a03-188">For the Key Vault sample application, the application owner sets these values in the app.config file.</span><span class="sxs-lookup"><span data-stu-id="f2a03-188">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="f2a03-189">To register the application in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="f2a03-189">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="f2a03-190">Sign in to the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="f2a03-190">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="f2a03-191">On the left, click **Active Directory**, and then select the directory in which you will register your application.</span><span class="sxs-lookup"><span data-stu-id="f2a03-191">On the left, click **Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> <span data-ttu-id="f2a03-192">**Note:** You must select the same directory that contains the Azure subscription with which you created your key vault.</span><span class="sxs-lookup"><span data-stu-id="f2a03-192">**Note:** You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="f2a03-193">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span><span class="sxs-lookup"><span data-stu-id="f2a03-193">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>
3. <span data-ttu-id="f2a03-194">Click **APPLICATIONS**.</span><span class="sxs-lookup"><span data-stu-id="f2a03-194">Click **APPLICATIONS**.</span></span> <span data-ttu-id="f2a03-195">If no apps have been added to your directory, this page shows only the **Add an App** link.</span><span class="sxs-lookup"><span data-stu-id="f2a03-195">If no apps have been added to your directory, this page shows only the **Add an App** link.</span></span> <span data-ttu-id="f2a03-196">Click the link, or alternatively, you can click **ADD** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="f2a03-196">Click the link, or alternatively, you can click **ADD** on the command bar.</span></span>
4. <span data-ttu-id="f2a03-197">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span><span class="sxs-lookup"><span data-stu-id="f2a03-197">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="f2a03-198">On the **Tell us about your application** page, specify a name for your application, and then select **WEB APPLICATION AND/OR WEB API** (the default).</span><span class="sxs-lookup"><span data-stu-id="f2a03-198">On the **Tell us about your application** page, specify a name for your application, and then select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="f2a03-199">Click the **Next** icon.</span><span class="sxs-lookup"><span data-stu-id="f2a03-199">Click the **Next** icon.</span></span>
6. <span data-ttu-id="f2a03-200">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span><span class="sxs-lookup"><span data-stu-id="f2a03-200">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="f2a03-201">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span><span class="sxs-lookup"><span data-stu-id="f2a03-201">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="f2a03-202">It does not matter if these sites exist.</span><span class="sxs-lookup"><span data-stu-id="f2a03-202">It does not matter if these sites exist.</span></span> <span data-ttu-id="f2a03-203">What is important is that the app ID URI for each application is different for every application in your directory.</span><span class="sxs-lookup"><span data-stu-id="f2a03-203">What is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="f2a03-204">The directory uses this string to identify your app.</span><span class="sxs-lookup"><span data-stu-id="f2a03-204">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="f2a03-205">Click the **Complete** icon to save your changes in the wizard.</span><span class="sxs-lookup"><span data-stu-id="f2a03-205">Click the **Complete** icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="f2a03-206">On the **Quick Start** page, click **CONFIGURE**.</span><span class="sxs-lookup"><span data-stu-id="f2a03-206">On the **Quick Start** page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="f2a03-207">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="f2a03-207">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="f2a03-208">The page refreshes and now shows a key value.</span><span class="sxs-lookup"><span data-stu-id="f2a03-208">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="f2a03-209">You must configure your application with this key value and the **CLIENT ID** value.</span><span class="sxs-lookup"><span data-stu-id="f2a03-209">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="f2a03-210">(Instructions for this configuration are application-specific.)</span><span class="sxs-lookup"><span data-stu-id="f2a03-210">(Instructions for this configuration are application-specific.)</span></span>
10. <span data-ttu-id="f2a03-211">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span><span class="sxs-lookup"><span data-stu-id="f2a03-211">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a id="authorize"></a><span data-ttu-id="f2a03-212">Authorize the application to use the key or secret</span><span class="sxs-lookup"><span data-stu-id="f2a03-212">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="f2a03-213">To authorize the application to access the key or secret in the vault, use the [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/azure/mt603625\(v=azure.300\).aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f2a03-213">To authorize the application to access the key or secret in the vault, use the [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/azure/mt603625\(v=azure.300\).aspx) cmdlet.</span></span>

<span data-ttu-id="f2a03-214">For example, if your vault name is **ContosoKeyVault** and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, run the following:</span><span class="sxs-lookup"><span data-stu-id="f2a03-214">For example, if your vault name is **ContosoKeyVault** and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, run the following:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

<span data-ttu-id="f2a03-215">If you want to authorize that same application to read secrets in your vault, run the following:</span><span class="sxs-lookup"><span data-stu-id="f2a03-215">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get

## <a id="HSM"></a><span data-ttu-id="f2a03-216">If you want to use a hardware security module (HSM)</span><span class="sxs-lookup"><span data-stu-id="f2a03-216">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="f2a03-217">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span><span class="sxs-lookup"><span data-stu-id="f2a03-217">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="f2a03-218">The HSMs are FIPS 140-2 Level 2 validated.</span><span class="sxs-lookup"><span data-stu-id="f2a03-218">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="f2a03-219">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete).</span><span class="sxs-lookup"><span data-stu-id="f2a03-219">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete).</span></span>

<span data-ttu-id="f2a03-220">To create these HSM-protected keys, you must use the [Azure Key Vault Premium service tier to support HSM-protected keys](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f2a03-220">To create these HSM-protected keys, you must use the [Azure Key Vault Premium service tier to support HSM-protected keys](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="f2a03-221">In addition, note that this functionality is not available for Azure China.</span><span class="sxs-lookup"><span data-stu-id="f2a03-221">In addition, note that this functionality is not available for Azure China.</span></span>

<span data-ttu-id="f2a03-222">When you create the key vault, add the **-SKU** parameter:</span><span class="sxs-lookup"><span data-stu-id="f2a03-222">When you create the key vault, add the **-SKU** parameter:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVaultHSM' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -SKU 'Premium'



<span data-ttu-id="f2a03-223">You can add software-protected keys (as shown earlier) and HSM-protected keys to this key vault.</span><span class="sxs-lookup"><span data-stu-id="f2a03-223">You can add software-protected keys (as shown earlier) and HSM-protected keys to this key vault.</span></span> <span data-ttu-id="f2a03-224">To create an HSM-protected key, set the **-Destination** parameter to 'HSM':</span><span class="sxs-lookup"><span data-stu-id="f2a03-224">To create an HSM-protected key, set the **-Destination** parameter to 'HSM':</span></span>

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -Destination 'HSM'

<span data-ttu-id="f2a03-225">You can use the following command to import a key from a .PFX file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f2a03-225">You can use the following command to import a key from a .PFX file on your computer.</span></span> <span data-ttu-id="f2a03-226">This command imports the key into HSMs in the Key Vault service:</span><span class="sxs-lookup"><span data-stu-id="f2a03-226">This command imports the key into HSMs in the Key Vault service:</span></span>

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd -Destination 'HSM'


<span data-ttu-id="f2a03-227">The next command imports a “bring your own key" (BYOK) package.</span><span class="sxs-lookup"><span data-stu-id="f2a03-227">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="f2a03-228">This scenario lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span><span class="sxs-lookup"><span data-stu-id="f2a03-228">This scenario lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\ITByok.byok' -Destination 'HSM'

<span data-ttu-id="f2a03-229">For more detailed instructions about how to generate this BYOK package, see [How to generate and transfer HSM-protected keys for Azure Key Vault](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="f2a03-229">For more detailed instructions about how to generate this BYOK package, see [How to generate and transfer HSM-protected keys for Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a id="delete"></a><span data-ttu-id="f2a03-230">Delete the key vault and associated keys and secrets</span><span class="sxs-lookup"><span data-stu-id="f2a03-230">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="f2a03-231">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the [Remove-AzureRmKeyVault](https://msdn.microsoft.com/library/azure/mt619485\(v=azure.300\).aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f2a03-231">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the [Remove-AzureRmKeyVault](https://msdn.microsoft.com/library/azure/mt619485\(v=azure.300\).aspx) cmdlet:</span></span>

    Remove-AzureRmKeyVault -VaultName 'ContosoKeyVault'

<span data-ttu-id="f2a03-232">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span><span class="sxs-lookup"><span data-stu-id="f2a03-232">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

    Remove-AzureRmResourceGroup -ResourceGroupName 'ContosoResourceGroup'


## <a id="other"></a><span data-ttu-id="f2a03-233">Other Azure PowerShell Cmdlets</span><span class="sxs-lookup"><span data-stu-id="f2a03-233">Other Azure PowerShell Cmdlets</span></span>
<span data-ttu-id="f2a03-234">Other commands that you might find useful for managing Azure Key Vault:</span><span class="sxs-lookup"><span data-stu-id="f2a03-234">Other commands that you might find useful for managing Azure Key Vault:</span></span>

* <span data-ttu-id="f2a03-235">`$Keys = Get-AzureKeyVaultKey -VaultName 'ContosoKeyVault'`: This command gets a tabular display of all keys and selected properties.</span><span class="sxs-lookup"><span data-stu-id="f2a03-235">`$Keys = Get-AzureKeyVaultKey -VaultName 'ContosoKeyVault'`: This command gets a tabular display of all keys and selected properties.</span></span>
* <span data-ttu-id="f2a03-236">`$Keys[0]`: This command displays a full list of properties for the specified key</span><span class="sxs-lookup"><span data-stu-id="f2a03-236">`$Keys[0]`: This command displays a full list of properties for the specified key</span></span>
* <span data-ttu-id="f2a03-237">`Get-AzureKeyVaultSecret`: This command lists a tabular display of all secret names and selected properties.</span><span class="sxs-lookup"><span data-stu-id="f2a03-237">`Get-AzureKeyVaultSecret`: This command lists a tabular display of all secret names and selected properties.</span></span>
* <span data-ttu-id="f2a03-238">`Remove-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey'`: Example how to remove a specific key.</span><span class="sxs-lookup"><span data-stu-id="f2a03-238">`Remove-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey'`: Example how to remove a specific key.</span></span>
* <span data-ttu-id="f2a03-239">`Remove-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword'`: Example how to remove a specific secret.</span><span class="sxs-lookup"><span data-stu-id="f2a03-239">`Remove-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword'`: Example how to remove a specific secret.</span></span>

## <a id="next"></a><span data-ttu-id="f2a03-240">Next steps</span><span class="sxs-lookup"><span data-stu-id="f2a03-240">Next steps</span></span>
<span data-ttu-id="f2a03-241">For a follow-up tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span><span class="sxs-lookup"><span data-stu-id="f2a03-241">For a follow-up tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="f2a03-242">To see how your key vault is being used, see [Azure Key Vault Logging](key-vault-logging.md).</span><span class="sxs-lookup"><span data-stu-id="f2a03-242">To see how your key vault is being used, see [Azure Key Vault Logging](key-vault-logging.md).</span></span>

<span data-ttu-id="f2a03-243">For a list of the latest Azure PowerShell cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](https://msdn.microsoft.com/library/azure/dn868052\(v=azure.300\).aspx).</span><span class="sxs-lookup"><span data-stu-id="f2a03-243">For a list of the latest Azure PowerShell cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](https://msdn.microsoft.com/library/azure/dn868052\(v=azure.300\).aspx).</span></span> 

<span data-ttu-id="f2a03-244">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="f2a03-244">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

