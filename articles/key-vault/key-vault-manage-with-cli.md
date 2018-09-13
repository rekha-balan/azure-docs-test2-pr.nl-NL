---
title: Manage Key Vault using CLI | Microsoft Docs
description: Use this tutorial to automate common tasks in Key Vault by using the CLI
services: key-vault
documentationcenter: ''
author: BrucePerlerMS
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 66be6e44-684a-411b-802e-884628458ae7
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: bruceper
ms.openlocfilehash: eec68b1cbfbddf0b72b55376ee11451b25898b68
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563387"
---
# <a name="manage-key-vault-using-cli"></a><span data-ttu-id="a98e0-103">Manage Key Vault using CLI</span><span class="sxs-lookup"><span data-stu-id="a98e0-103">Manage Key Vault using CLI</span></span>
<span data-ttu-id="a98e0-104">Azure Key Vault is available in most regions.</span><span class="sxs-lookup"><span data-stu-id="a98e0-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="a98e0-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="a98e0-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="a98e0-106">Introduction</span><span class="sxs-lookup"><span data-stu-id="a98e0-106">Introduction</span></span>
<span data-ttu-id="a98e0-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span><span class="sxs-lookup"><span data-stu-id="a98e0-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="a98e0-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span><span class="sxs-lookup"><span data-stu-id="a98e0-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="a98e0-109">It then shows you how an application can then use that key or password.</span><span class="sxs-lookup"><span data-stu-id="a98e0-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="a98e0-110">**Estimated time to complete:** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="a98e0-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="a98e0-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span><span class="sxs-lookup"><span data-stu-id="a98e0-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
> 
> <span data-ttu-id="a98e0-112">Currently, you cannot configure Azure Key Vault in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a98e0-112">Currently, you cannot configure Azure Key Vault in the Azure portal.</span></span> <span data-ttu-id="a98e0-113">Instead, use these Cross-Platform Command-Line Interface  instructions.</span><span class="sxs-lookup"><span data-stu-id="a98e0-113">Instead, use these Cross-Platform Command-Line Interface  instructions.</span></span> <span data-ttu-id="a98e0-114">Or, for Azure PowerShell instructions, see [this equivalent tutorial](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a98e0-114">Or, for Azure PowerShell instructions, see [this equivalent tutorial](key-vault-get-started.md).</span></span>
> 
> 

<span data-ttu-id="a98e0-115">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="a98e0-115">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a98e0-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a98e0-116">Prerequisites</span></span>
<span data-ttu-id="a98e0-117">To complete this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="a98e0-117">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="a98e0-118">A subscription to Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a98e0-118">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="a98e0-119">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="a98e0-119">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="a98e0-120">Command-Line Interface version 0.9.1 or later.</span><span class="sxs-lookup"><span data-stu-id="a98e0-120">Command-Line Interface version 0.9.1 or later.</span></span> <span data-ttu-id="a98e0-121">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a98e0-121">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="a98e0-122">An application that will be configured to use the key or password that you create in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="a98e0-122">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="a98e0-123">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="a98e0-123">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="a98e0-124">For instructions, see the accompanying Readme file.</span><span class="sxs-lookup"><span data-stu-id="a98e0-124">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="a98e0-125">Getting help with Azure Cross-Platform Command-Line Interface</span><span class="sxs-lookup"><span data-stu-id="a98e0-125">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="a98e0-126">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span><span class="sxs-lookup"><span data-stu-id="a98e0-126">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="a98e0-127">The --help or -h parameter can be used to view help for specific commands.</span><span class="sxs-lookup"><span data-stu-id="a98e0-127">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="a98e0-128">Alternately, The azure help [command] [options] format can also be used to return the same information.</span><span class="sxs-lookup"><span data-stu-id="a98e0-128">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="a98e0-129">For example, the following commands all return the same information:</span><span class="sxs-lookup"><span data-stu-id="a98e0-129">For example, the following commands all return the same information:</span></span>

    azure account set --help

    azure account set -h

    azure help account set

<span data-ttu-id="a98e0-130">When in doubt about the parameters needed by a command, refer to help using --help, -h or azure help [command].</span><span class="sxs-lookup"><span data-stu-id="a98e0-130">When in doubt about the parameters needed by a command, refer to help using --help, -h or azure help [command].</span></span>

<span data-ttu-id="a98e0-131">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span><span class="sxs-lookup"><span data-stu-id="a98e0-131">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="a98e0-132">How to install and configure Azure Cross-Platform Command Line Interface</span><span class="sxs-lookup"><span data-stu-id="a98e0-132">How to install and configure Azure Cross-Platform Command Line Interface</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="a98e0-133">Using Azure Cross-Platform Command-Line Interface with Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a98e0-133">Using Azure Cross-Platform Command-Line Interface with Azure Resource Manager</span></span>](../xplat-cli-azure-resource-manager.md)

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="a98e0-134">Connect to your subscriptions</span><span class="sxs-lookup"><span data-stu-id="a98e0-134">Connect to your subscriptions</span></span>
<span data-ttu-id="a98e0-135">To log in using an organizational account, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a98e0-135">To log in using an organizational account, use the following command:</span></span>

    azure login -u username -p password

<span data-ttu-id="a98e0-136">or if you want to log in by typing interactively</span><span class="sxs-lookup"><span data-stu-id="a98e0-136">or if you want to log in by typing interactively</span></span>

    azure login

> [!NOTE]
> <span data-ttu-id="a98e0-137">The login method only works with organizational account.</span><span class="sxs-lookup"><span data-stu-id="a98e0-137">The login method only works with organizational account.</span></span> <span data-ttu-id="a98e0-138">An organizational account is a user that is managed by your organization, and defined in your organization's Azure Active Directory tenant.</span><span class="sxs-lookup"><span data-stu-id="a98e0-138">An organizational account is a user that is managed by your organization, and defined in your organization's Azure Active Directory tenant.</span></span>
> 
> 

<span data-ttu-id="a98e0-139">If you do not currently have an organizational account, and are using a Microsoft account to log in to your Azure subscription, you can easily create one using the following steps.</span><span class="sxs-lookup"><span data-stu-id="a98e0-139">If you do not currently have an organizational account, and are using a Microsoft account to log in to your Azure subscription, you can easily create one using the following steps.</span></span>

1. <span data-ttu-id="a98e0-140">Login to the Login to the [Azure Management Portal](https://manage.windowsazure.com/), and click on Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a98e0-140">Login to the Login to the [Azure Management Portal](https://manage.windowsazure.com/), and click on Active Directory.</span></span>
2. <span data-ttu-id="a98e0-141">If no directory exists, select Create your directory and provide the requested information.</span><span class="sxs-lookup"><span data-stu-id="a98e0-141">If no directory exists, select Create your directory and provide the requested information.</span></span>
3. <span data-ttu-id="a98e0-142">Select your directory and add a new user.</span><span class="sxs-lookup"><span data-stu-id="a98e0-142">Select your directory and add a new user.</span></span> <span data-ttu-id="a98e0-143">This new user is an organizational account.</span><span class="sxs-lookup"><span data-stu-id="a98e0-143">This new user is an organizational account.</span></span> <span data-ttu-id="a98e0-144">During the creation of the user, you will be supplied with both an e-mail address for the user and a temporary password.</span><span class="sxs-lookup"><span data-stu-id="a98e0-144">During the creation of the user, you will be supplied with both an e-mail address for the user and a temporary password.</span></span> <span data-ttu-id="a98e0-145">Save this information as it is used in another step.</span><span class="sxs-lookup"><span data-stu-id="a98e0-145">Save this information as it is used in another step.</span></span>
4. <span data-ttu-id="a98e0-146">From the portal, select Settings and then select Administrators.</span><span class="sxs-lookup"><span data-stu-id="a98e0-146">From the portal, select Settings and then select Administrators.</span></span> <span data-ttu-id="a98e0-147">Select Add, and add the new user as a co-administrator.</span><span class="sxs-lookup"><span data-stu-id="a98e0-147">Select Add, and add the new user as a co-administrator.</span></span> <span data-ttu-id="a98e0-148">This allows the organizational account to manage your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a98e0-148">This allows the organizational account to manage your Azure subscription.</span></span>
5. <span data-ttu-id="a98e0-149">Finally, log out of the Azure portal and then log back in using the new organizational account.</span><span class="sxs-lookup"><span data-stu-id="a98e0-149">Finally, log out of the Azure portal and then log back in using the new organizational account.</span></span> <span data-ttu-id="a98e0-150">If this is the first time logging in with this account, you will be prompted to change the password.</span><span class="sxs-lookup"><span data-stu-id="a98e0-150">If this is the first time logging in with this account, you will be prompted to change the password.</span></span>

<span data-ttu-id="a98e0-151">For more information about using an organizational account with Microsoft Azure, see [Sign up for Microsoft Azure as an Organization](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="a98e0-151">For more information about using an organizational account with Microsoft Azure, see [Sign up for Microsoft Azure as an Organization](../active-directory/sign-up-organization.md).</span></span>

<span data-ttu-id="a98e0-152">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span><span class="sxs-lookup"><span data-stu-id="a98e0-152">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

    azure account list

<span data-ttu-id="a98e0-153">Then, to specify the subscription to use, type:</span><span class="sxs-lookup"><span data-stu-id="a98e0-153">Then, to specify the subscription to use, type:</span></span>

    azure account set <subscription name>

<span data-ttu-id="a98e0-154">For more information about configuring Azure Cross-Platform Command-Line Interface, see [How to Install and Configure Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a98e0-154">For more information about configuring Azure Cross-Platform Command-Line Interface, see [How to Install and Configure Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>

## <a name="switch-to-using-azure-resource-manager"></a><span data-ttu-id="a98e0-155">Switch to using Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a98e0-155">Switch to using Azure Resource Manager</span></span>
<span data-ttu-id="a98e0-156">The Key Vault requires Azure Resource Manager, so type the following to switch to Azure Resource Manager mode:</span><span class="sxs-lookup"><span data-stu-id="a98e0-156">The Key Vault requires Azure Resource Manager, so type the following to switch to Azure Resource Manager mode:</span></span>

    azure config mode arm

## <a name="create-a-new-resource-group"></a><span data-ttu-id="a98e0-157">Create a new resource group</span><span class="sxs-lookup"><span data-stu-id="a98e0-157">Create a new resource group</span></span>
<span data-ttu-id="a98e0-158">When using Azure Resource Manager, all related resources are created inside a resource group.</span><span class="sxs-lookup"><span data-stu-id="a98e0-158">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="a98e0-159">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="a98e0-159">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

    azure group create 'ContosoResourceGroup' 'East Asia'

<span data-ttu-id="a98e0-160">The first parameter is resource group name and the second parameter is the location.</span><span class="sxs-lookup"><span data-stu-id="a98e0-160">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="a98e0-161">For location, use the command `azure location list` to identify how to specify an alternative location to the one in this example.</span><span class="sxs-lookup"><span data-stu-id="a98e0-161">For location, use the command `azure location list` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="a98e0-162">If you need more information, type: `azure help location`</span><span class="sxs-lookup"><span data-stu-id="a98e0-162">If you need more information, type: `azure help location`</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="a98e0-163">Register the Key Vault resource provider</span><span class="sxs-lookup"><span data-stu-id="a98e0-163">Register the Key Vault resource provider</span></span>
<span data-ttu-id="a98e0-164">Make sure that Key Vault resource provider is registered in your subscription:</span><span class="sxs-lookup"><span data-stu-id="a98e0-164">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

`azure provider register Microsoft.KeyVault`

<span data-ttu-id="a98e0-165">This only needs to be done once per subscription.</span><span class="sxs-lookup"><span data-stu-id="a98e0-165">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="a98e0-166">Create a key vault</span><span class="sxs-lookup"><span data-stu-id="a98e0-166">Create a key vault</span></span>
<span data-ttu-id="a98e0-167">Use the `azure keyvault create` command to create a key vault.</span><span class="sxs-lookup"><span data-stu-id="a98e0-167">Use the `azure keyvault create` command to create a key vault.</span></span> <span data-ttu-id="a98e0-168">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span><span class="sxs-lookup"><span data-stu-id="a98e0-168">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="a98e0-169">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span><span class="sxs-lookup"><span data-stu-id="a98e0-169">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

<span data-ttu-id="a98e0-170">The output of this command shows properties of the key vault that you've just created.</span><span class="sxs-lookup"><span data-stu-id="a98e0-170">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="a98e0-171">The two most important properties are:</span><span class="sxs-lookup"><span data-stu-id="a98e0-171">The two most important properties are:</span></span>

* <span data-ttu-id="a98e0-172">**Name**: In the example this is ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="a98e0-172">**Name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="a98e0-173">You will use this name for other Key Vault cmdlets.</span><span class="sxs-lookup"><span data-stu-id="a98e0-173">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="a98e0-174">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="a98e0-174">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="a98e0-175">Applications that use your vault through its REST API must use this URI.</span><span class="sxs-lookup"><span data-stu-id="a98e0-175">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="a98e0-176">Your Azure account is now authorized to perform any operations on this key vault.</span><span class="sxs-lookup"><span data-stu-id="a98e0-176">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="a98e0-177">As yet, nobody else is.</span><span class="sxs-lookup"><span data-stu-id="a98e0-177">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="a98e0-178">Add a key or secret to the key vault</span><span class="sxs-lookup"><span data-stu-id="a98e0-178">Add a key or secret to the key vault</span></span>
<span data-ttu-id="a98e0-179">If you want Azure Key Vault to create a software-protected key for you, use the `azure key create` command, and type the following:</span><span class="sxs-lookup"><span data-stu-id="a98e0-179">If you want Azure Key Vault to create a software-protected key for you, use the `azure key create` command, and type the following:</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

<span data-ttu-id="a98e0-180">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span><span class="sxs-lookup"><span data-stu-id="a98e0-180">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

<span data-ttu-id="a98e0-181">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span><span class="sxs-lookup"><span data-stu-id="a98e0-181">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="a98e0-182">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span><span class="sxs-lookup"><span data-stu-id="a98e0-182">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="a98e0-183">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span><span class="sxs-lookup"><span data-stu-id="a98e0-183">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

<span data-ttu-id="a98e0-184">You can now reference this password that you added to Azure Key Vault, by using its URI.</span><span class="sxs-lookup"><span data-stu-id="a98e0-184">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="a98e0-185">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span><span class="sxs-lookup"><span data-stu-id="a98e0-185">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="a98e0-186">Let's view the key or secret that you just created:</span><span class="sxs-lookup"><span data-stu-id="a98e0-186">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="a98e0-187">To view your key, type: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="a98e0-187">To view your key, type: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="a98e0-188">To view your secret, type: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="a98e0-188">To view your secret, type: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="a98e0-189">Register an application with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a98e0-189">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="a98e0-190">This step would usually be done by a developer, on a separate computer.</span><span class="sxs-lookup"><span data-stu-id="a98e0-190">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="a98e0-191">It is not specific to Azure Key Vault but is included here, for completeness.</span><span class="sxs-lookup"><span data-stu-id="a98e0-191">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a98e0-192">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span><span class="sxs-lookup"><span data-stu-id="a98e0-192">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
> 
> 

<span data-ttu-id="a98e0-193">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a98e0-193">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="a98e0-194">To do this, the owner of the application must first register the application in their Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a98e0-194">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="a98e0-195">At the end of registration, the application owner gets the following values:</span><span class="sxs-lookup"><span data-stu-id="a98e0-195">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="a98e0-196">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span><span class="sxs-lookup"><span data-stu-id="a98e0-196">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="a98e0-197">The application must present both of these values to Azure Active Directory, to get a token.</span><span class="sxs-lookup"><span data-stu-id="a98e0-197">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="a98e0-198">How the application is configured to do this depends on the application.</span><span class="sxs-lookup"><span data-stu-id="a98e0-198">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="a98e0-199">For the Key Vault sample application, the application owner sets these values in the app.config file.</span><span class="sxs-lookup"><span data-stu-id="a98e0-199">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="a98e0-200">To register the application in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="a98e0-200">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="a98e0-201">Sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a98e0-201">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="a98e0-202">On the left, click **Active Directory**, and then select the directory in which you will register your application.</span><span class="sxs-lookup"><span data-stu-id="a98e0-202">On the left, click **Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> <span data-ttu-id="a98e0-203">Note: You must select the same directory that contains the Azure subscription with which you created your key vault.</span><span class="sxs-lookup"><span data-stu-id="a98e0-203">Note: You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="a98e0-204">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span><span class="sxs-lookup"><span data-stu-id="a98e0-204">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>
3. <span data-ttu-id="a98e0-205">Click **APPLICATIONS**.</span><span class="sxs-lookup"><span data-stu-id="a98e0-205">Click **APPLICATIONS**.</span></span> <span data-ttu-id="a98e0-206">If no apps have been added to your directory, this page will show only the **Add an App** link.</span><span class="sxs-lookup"><span data-stu-id="a98e0-206">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="a98e0-207">Click the link, or alternatively, you can click the **ADD** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="a98e0-207">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="a98e0-208">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span><span class="sxs-lookup"><span data-stu-id="a98e0-208">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="a98e0-209">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span><span class="sxs-lookup"><span data-stu-id="a98e0-209">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="a98e0-210">Click the Next icon.</span><span class="sxs-lookup"><span data-stu-id="a98e0-210">Click the Next icon.</span></span>
6. <span data-ttu-id="a98e0-211">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span><span class="sxs-lookup"><span data-stu-id="a98e0-211">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="a98e0-212">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span><span class="sxs-lookup"><span data-stu-id="a98e0-212">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="a98e0-213">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span><span class="sxs-lookup"><span data-stu-id="a98e0-213">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="a98e0-214">The directory uses this string to identify your app.</span><span class="sxs-lookup"><span data-stu-id="a98e0-214">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="a98e0-215">Click the Complete icon to save your changes in the wizard.</span><span class="sxs-lookup"><span data-stu-id="a98e0-215">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="a98e0-216">On the Quick Start page, click **CONFIGURE**.</span><span class="sxs-lookup"><span data-stu-id="a98e0-216">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="a98e0-217">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="a98e0-217">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="a98e0-218">The page refreshes and now shows a key value.</span><span class="sxs-lookup"><span data-stu-id="a98e0-218">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="a98e0-219">You must configure your application with this key value and the **CLIENT ID** value.</span><span class="sxs-lookup"><span data-stu-id="a98e0-219">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="a98e0-220">(Instructions for this configuration will be application-specific.)</span><span class="sxs-lookup"><span data-stu-id="a98e0-220">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="a98e0-221">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span><span class="sxs-lookup"><span data-stu-id="a98e0-221">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="a98e0-222">Authorize the application to use the key or secret</span><span class="sxs-lookup"><span data-stu-id="a98e0-222">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="a98e0-223">To authorize the application to access the key or secret in the vault, use the `azure keyvault set-policy` command.</span><span class="sxs-lookup"><span data-stu-id="a98e0-223">To authorize the application to access the key or secret in the vault, use the `azure keyvault set-policy` command.</span></span>

<span data-ttu-id="a98e0-224">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span><span class="sxs-lookup"><span data-stu-id="a98e0-224">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '["decrypt","sign"]'

> [!NOTE]
> <span data-ttu-id="a98e0-225">If you are running on Windows command prompt, you should replace single quotes with double quotes, and also escape the internal double quotes.</span><span class="sxs-lookup"><span data-stu-id="a98e0-225">If you are running on Windows command prompt, you should replace single quotes with double quotes, and also escape the internal double quotes.</span></span> <span data-ttu-id="a98e0-226">For example: "[\"decrypt\",\"sign\"]".</span><span class="sxs-lookup"><span data-stu-id="a98e0-226">For example: "[\"decrypt\",\"sign\"]".</span></span>
> 
> 

<span data-ttu-id="a98e0-227">If you want to authorize that same application to read secrets in your vault, run the following:</span><span class="sxs-lookup"><span data-stu-id="a98e0-227">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '["get"]'

## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="a98e0-228">If you want to use a hardware security module (HSM)</span><span class="sxs-lookup"><span data-stu-id="a98e0-228">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="a98e0-229">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span><span class="sxs-lookup"><span data-stu-id="a98e0-229">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="a98e0-230">The HSMs are FIPS 140-2 Level 2 validated.</span><span class="sxs-lookup"><span data-stu-id="a98e0-230">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="a98e0-231">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="a98e0-231">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="a98e0-232">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span><span class="sxs-lookup"><span data-stu-id="a98e0-232">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="a98e0-233">When you create the keyvault, add the 'sku' parameter:</span><span class="sxs-lookup"><span data-stu-id="a98e0-233">When you create the keyvault, add the 'sku' parameter:</span></span>

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

<span data-ttu-id="a98e0-234">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span><span class="sxs-lookup"><span data-stu-id="a98e0-234">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="a98e0-235">To create an HSM-protected key, set the Destination parameter to 'HSM':</span><span class="sxs-lookup"><span data-stu-id="a98e0-235">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

<span data-ttu-id="a98e0-236">You can use the following command to import a key from a .pem file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a98e0-236">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="a98e0-237">This command imports the key into HSMs in the Key Vault service:</span><span class="sxs-lookup"><span data-stu-id="a98e0-237">This command imports the key into HSMs in the Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

<span data-ttu-id="a98e0-238">The next command imports a “bring your own key" (BYOK) package.</span><span class="sxs-lookup"><span data-stu-id="a98e0-238">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="a98e0-239">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span><span class="sxs-lookup"><span data-stu-id="a98e0-239">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

<span data-ttu-id="a98e0-240">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="a98e0-240">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="a98e0-241">Delete the key vault and associated keys and secrets</span><span class="sxs-lookup"><span data-stu-id="a98e0-241">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="a98e0-242">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the azure keyvault delete command:</span><span class="sxs-lookup"><span data-stu-id="a98e0-242">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the azure keyvault delete command:</span></span>

    azure keyvault delete --vault-name 'ContosoKeyVault'

<span data-ttu-id="a98e0-243">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span><span class="sxs-lookup"><span data-stu-id="a98e0-243">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="a98e0-244">Other Azure Cross-Platform Command-line Interface Commands</span><span class="sxs-lookup"><span data-stu-id="a98e0-244">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="a98e0-245">Other commands that you might useful for managing Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="a98e0-245">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="a98e0-246">This command lists a tabular display of all keys and selected properties:</span><span class="sxs-lookup"><span data-stu-id="a98e0-246">This command lists a tabular display of all keys and selected properties:</span></span>

    azure keyvault key list --vault-name 'ContosoKeyVault'

<span data-ttu-id="a98e0-247">This command displays a full list of properties for the specified key:</span><span class="sxs-lookup"><span data-stu-id="a98e0-247">This command displays a full list of properties for the specified key:</span></span>

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="a98e0-248">This command lists a tabular display of all secret names and selected properties:</span><span class="sxs-lookup"><span data-stu-id="a98e0-248">This command lists a tabular display of all secret names and selected properties:</span></span>

    azure keyvault secret list --vault-name 'ContosoKeyVault'

<span data-ttu-id="a98e0-249">Here's an example of how to remove a specific key:</span><span class="sxs-lookup"><span data-stu-id="a98e0-249">Here's an example of how to remove a specific key:</span></span>

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="a98e0-250">Here's an example of how to remove a specific secret:</span><span class="sxs-lookup"><span data-stu-id="a98e0-250">Here's an example of how to remove a specific secret:</span></span>

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a><span data-ttu-id="a98e0-251">Next steps</span><span class="sxs-lookup"><span data-stu-id="a98e0-251">Next steps</span></span>
<span data-ttu-id="a98e0-252">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="a98e0-252">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

