---
title: Manage Key Vault using CLI | Microsoft Docs
description: Use this tutorial to automate common tasks in Key Vault by using the CLI 2.0
services: key-vault
documentationcenter: ''
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: ''
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 24b56848523a9bd7145e1c99394d55b9708e9896
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556724"
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="77a06-103">Manage Key Vault using CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="77a06-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="77a06-104">Azure Key Vault is available in most regions.</span><span class="sxs-lookup"><span data-stu-id="77a06-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="77a06-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="77a06-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="77a06-106">Introduction</span><span class="sxs-lookup"><span data-stu-id="77a06-106">Introduction</span></span>
<span data-ttu-id="77a06-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span><span class="sxs-lookup"><span data-stu-id="77a06-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="77a06-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span><span class="sxs-lookup"><span data-stu-id="77a06-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="77a06-109">It then shows you how an application can then use that key or password.</span><span class="sxs-lookup"><span data-stu-id="77a06-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="77a06-110">**Estimated time to complete:** 20 minutes</span><span class="sxs-lookup"><span data-stu-id="77a06-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="77a06-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span><span class="sxs-lookup"><span data-stu-id="77a06-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
>
> <span data-ttu-id="77a06-112">This tutorial uses the latest Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="77a06-112">This tutorial uses the latest Azure CLI 2.0.</span></span> <span data-ttu-id="77a06-113">For instructions using older (node.js based) CLI refer to [this equivalent tutorial](key-vault-manage-with-cli.md).</span><span class="sxs-lookup"><span data-stu-id="77a06-113">For instructions using older (node.js based) CLI refer to [this equivalent tutorial](key-vault-manage-with-cli.md).</span></span>
>
>

<span data-ttu-id="77a06-114">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="77a06-114">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77a06-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="77a06-115">Prerequisites</span></span>
<span data-ttu-id="77a06-116">To complete this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="77a06-116">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="77a06-117">A subscription to Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="77a06-117">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="77a06-118">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="77a06-118">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="77a06-119">Command-Line Interface version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="77a06-119">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="77a06-120">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="77a06-120">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="77a06-121">An application that will be configured to use the key or password that you create in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="77a06-121">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="77a06-122">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="77a06-122">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="77a06-123">For instructions, see the accompanying Readme file.</span><span class="sxs-lookup"><span data-stu-id="77a06-123">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="77a06-124">Getting help with Azure Cross-Platform Command-Line Interface</span><span class="sxs-lookup"><span data-stu-id="77a06-124">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="77a06-125">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span><span class="sxs-lookup"><span data-stu-id="77a06-125">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="77a06-126">The --help or -h parameter can be used to view help for specific commands.</span><span class="sxs-lookup"><span data-stu-id="77a06-126">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="77a06-127">Alternately, The azure help [command] [options] format can also be used to return the same information.</span><span class="sxs-lookup"><span data-stu-id="77a06-127">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="77a06-128">For example, the following commands all return the same information:</span><span class="sxs-lookup"><span data-stu-id="77a06-128">For example, the following commands all return the same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="77a06-129">When in doubt about the parameters needed by a command, refer to help using --help, -h or az help [command].</span><span class="sxs-lookup"><span data-stu-id="77a06-129">When in doubt about the parameters needed by a command, refer to help using --help, -h or az help [command].</span></span>

<span data-ttu-id="77a06-130">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span><span class="sxs-lookup"><span data-stu-id="77a06-130">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="77a06-131">Install Azure CLI</span><span class="sxs-lookup"><span data-stu-id="77a06-131">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* [<span data-ttu-id="77a06-132">Get started with Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="77a06-132">Get started with Azure CLI 2.0</span></span>](/cli/azure/get-started-with-azure-cli)

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="77a06-133">Connect to your subscriptions</span><span class="sxs-lookup"><span data-stu-id="77a06-133">Connect to your subscriptions</span></span>
<span data-ttu-id="77a06-134">To log in using an organizational account, use the following command:</span><span class="sxs-lookup"><span data-stu-id="77a06-134">To log in using an organizational account, use the following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="77a06-135">or if you want to log in by typing interactively</span><span class="sxs-lookup"><span data-stu-id="77a06-135">or if you want to log in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="77a06-136">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span><span class="sxs-lookup"><span data-stu-id="77a06-136">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="77a06-137">Then, to specify the subscription to use, type:</span><span class="sxs-lookup"><span data-stu-id="77a06-137">Then, to specify the subscription to use, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="77a06-138">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="77a06-138">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="77a06-139">Create a new resource group</span><span class="sxs-lookup"><span data-stu-id="77a06-139">Create a new resource group</span></span>
<span data-ttu-id="77a06-140">When using Azure Resource Manager, all related resources are created inside a resource group.</span><span class="sxs-lookup"><span data-stu-id="77a06-140">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="77a06-141">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="77a06-141">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="77a06-142">The first parameter is resource group name and the second parameter is the location.</span><span class="sxs-lookup"><span data-stu-id="77a06-142">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="77a06-143">For location, use the command `az account list-locations` to identify how to specify an alternative location to the one in this example.</span><span class="sxs-lookup"><span data-stu-id="77a06-143">For location, use the command `az account list-locations` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="77a06-144">If you need more information, type: `az account list-locations -h`.</span><span class="sxs-lookup"><span data-stu-id="77a06-144">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="77a06-145">Register the Key Vault resource provider</span><span class="sxs-lookup"><span data-stu-id="77a06-145">Register the Key Vault resource provider</span></span>
<span data-ttu-id="77a06-146">Make sure that Key Vault resource provider is registered in your subscription:</span><span class="sxs-lookup"><span data-stu-id="77a06-146">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="77a06-147">This only needs to be done once per subscription.</span><span class="sxs-lookup"><span data-stu-id="77a06-147">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="77a06-148">Create a key vault</span><span class="sxs-lookup"><span data-stu-id="77a06-148">Create a key vault</span></span>
<span data-ttu-id="77a06-149">Use the `az keyvault create` command to create a key vault.</span><span class="sxs-lookup"><span data-stu-id="77a06-149">Use the `az keyvault create` command to create a key vault.</span></span> <span data-ttu-id="77a06-150">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span><span class="sxs-lookup"><span data-stu-id="77a06-150">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="77a06-151">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span><span class="sxs-lookup"><span data-stu-id="77a06-151">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="77a06-152">The output of this command shows properties of the key vault that you've just created.</span><span class="sxs-lookup"><span data-stu-id="77a06-152">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="77a06-153">The two most important properties are:</span><span class="sxs-lookup"><span data-stu-id="77a06-153">The two most important properties are:</span></span>

* <span data-ttu-id="77a06-154">**name**: In the example this is ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="77a06-154">**name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="77a06-155">You will use this name for other Key Vault commands.</span><span class="sxs-lookup"><span data-stu-id="77a06-155">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="77a06-156">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="77a06-156">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="77a06-157">Applications that use your vault through its REST API must use this URI.</span><span class="sxs-lookup"><span data-stu-id="77a06-157">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="77a06-158">Your Azure account is now authorized to perform any operations on this key vault.</span><span class="sxs-lookup"><span data-stu-id="77a06-158">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="77a06-159">As yet, nobody else is.</span><span class="sxs-lookup"><span data-stu-id="77a06-159">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="77a06-160">Add a key or secret to the key vault</span><span class="sxs-lookup"><span data-stu-id="77a06-160">Add a key or secret to the key vault</span></span>
<span data-ttu-id="77a06-161">If you want Azure Key Vault to create a software-protected key for you, use the `az key create` command, and type the following:</span><span class="sxs-lookup"><span data-stu-id="77a06-161">If you want Azure Key Vault to create a software-protected key for you, use the `az key create` command, and type the following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="77a06-162">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span><span class="sxs-lookup"><span data-stu-id="77a06-162">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="77a06-163">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span><span class="sxs-lookup"><span data-stu-id="77a06-163">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="77a06-164">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span><span class="sxs-lookup"><span data-stu-id="77a06-164">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="77a06-165">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span><span class="sxs-lookup"><span data-stu-id="77a06-165">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="77a06-166">You can now reference this password that you added to Azure Key Vault, by using its URI.</span><span class="sxs-lookup"><span data-stu-id="77a06-166">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="77a06-167">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span><span class="sxs-lookup"><span data-stu-id="77a06-167">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="77a06-168">Let's view the key or secret that you just created:</span><span class="sxs-lookup"><span data-stu-id="77a06-168">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="77a06-169">To view your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="77a06-169">To view your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="77a06-170">To view your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="77a06-170">To view your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="77a06-171">Register an application with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77a06-171">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="77a06-172">This step would usually be done by a developer, on a separate computer.</span><span class="sxs-lookup"><span data-stu-id="77a06-172">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="77a06-173">It is not specific to Azure Key Vault but is included here, for completeness.</span><span class="sxs-lookup"><span data-stu-id="77a06-173">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77a06-174">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span><span class="sxs-lookup"><span data-stu-id="77a06-174">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
>
>

<span data-ttu-id="77a06-175">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="77a06-175">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="77a06-176">To do this, the owner of the application must first register the application in their Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="77a06-176">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="77a06-177">At the end of registration, the application owner gets the following values:</span><span class="sxs-lookup"><span data-stu-id="77a06-177">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="77a06-178">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span><span class="sxs-lookup"><span data-stu-id="77a06-178">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="77a06-179">The application must present both of these values to Azure Active Directory, to get a token.</span><span class="sxs-lookup"><span data-stu-id="77a06-179">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="77a06-180">How the application is configured to do this depends on the application.</span><span class="sxs-lookup"><span data-stu-id="77a06-180">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="77a06-181">For the Key Vault sample application, the application owner sets these values in the app.config file.</span><span class="sxs-lookup"><span data-stu-id="77a06-181">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="77a06-182">To register the application in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="77a06-182">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="77a06-183">Sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="77a06-183">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="77a06-184">On the left, click **Azure Active Directory**, and then select the directory in which you will register your application.</span><span class="sxs-lookup"><span data-stu-id="77a06-184">On the left, click **Azure Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> <span data-ttu-id="77a06-185">Note: You must select the same directory that contains the Azure subscription with which you created your key vault.</span><span class="sxs-lookup"><span data-stu-id="77a06-185">Note: You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="77a06-186">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span><span class="sxs-lookup"><span data-stu-id="77a06-186">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>
3. <span data-ttu-id="77a06-187">Click **APPLICATIONS**.</span><span class="sxs-lookup"><span data-stu-id="77a06-187">Click **APPLICATIONS**.</span></span> <span data-ttu-id="77a06-188">If no apps have been added to your directory, this page will show only the **Add an App** link.</span><span class="sxs-lookup"><span data-stu-id="77a06-188">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="77a06-189">Click the link, or alternatively, you can click the **ADD** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="77a06-189">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="77a06-190">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span><span class="sxs-lookup"><span data-stu-id="77a06-190">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="77a06-191">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span><span class="sxs-lookup"><span data-stu-id="77a06-191">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="77a06-192">Click the Next icon.</span><span class="sxs-lookup"><span data-stu-id="77a06-192">Click the Next icon.</span></span>
6. <span data-ttu-id="77a06-193">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span><span class="sxs-lookup"><span data-stu-id="77a06-193">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="77a06-194">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span><span class="sxs-lookup"><span data-stu-id="77a06-194">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="77a06-195">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span><span class="sxs-lookup"><span data-stu-id="77a06-195">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="77a06-196">The directory uses this string to identify your app.</span><span class="sxs-lookup"><span data-stu-id="77a06-196">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="77a06-197">Click the Complete icon to save your changes in the wizard.</span><span class="sxs-lookup"><span data-stu-id="77a06-197">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="77a06-198">On the Quick Start page, click **CONFIGURE**.</span><span class="sxs-lookup"><span data-stu-id="77a06-198">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="77a06-199">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="77a06-199">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="77a06-200">The page refreshes and now shows a key value.</span><span class="sxs-lookup"><span data-stu-id="77a06-200">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="77a06-201">You must configure your application with this key value and the **CLIENT ID** value.</span><span class="sxs-lookup"><span data-stu-id="77a06-201">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="77a06-202">(Instructions for this configuration will be application-specific.)</span><span class="sxs-lookup"><span data-stu-id="77a06-202">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="77a06-203">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span><span class="sxs-lookup"><span data-stu-id="77a06-203">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="77a06-204">Authorize the application to use the key or secret</span><span class="sxs-lookup"><span data-stu-id="77a06-204">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="77a06-205">To authorize the application to access the key or secret in the vault, use the `az keyvault set-policy` command.</span><span class="sxs-lookup"><span data-stu-id="77a06-205">To authorize the application to access the key or secret in the vault, use the `az keyvault set-policy` command.</span></span>

<span data-ttu-id="77a06-206">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span><span class="sxs-lookup"><span data-stu-id="77a06-206">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="77a06-207">If you want to authorize that same application to read secrets in your vault, run the following:</span><span class="sxs-lookup"><span data-stu-id="77a06-207">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="77a06-208">If you want to use a hardware security module (HSM)</span><span class="sxs-lookup"><span data-stu-id="77a06-208">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="77a06-209">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span><span class="sxs-lookup"><span data-stu-id="77a06-209">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="77a06-210">The HSMs are FIPS 140-2 Level 2 validated.</span><span class="sxs-lookup"><span data-stu-id="77a06-210">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="77a06-211">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="77a06-211">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="77a06-212">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span><span class="sxs-lookup"><span data-stu-id="77a06-212">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="77a06-213">When you create the keyvault, add the 'sku' parameter:</span><span class="sxs-lookup"><span data-stu-id="77a06-213">When you create the keyvault, add the 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="77a06-214">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span><span class="sxs-lookup"><span data-stu-id="77a06-214">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="77a06-215">To create an HSM-protected key, set the Destination parameter to 'HSM':</span><span class="sxs-lookup"><span data-stu-id="77a06-215">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="77a06-216">You can use the following command to import a key from a .pem file on your computer.</span><span class="sxs-lookup"><span data-stu-id="77a06-216">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="77a06-217">This command imports the key into HSMs in the Key Vault service:</span><span class="sxs-lookup"><span data-stu-id="77a06-217">This command imports the key into HSMs in the Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="77a06-218">The next command imports a “bring your own key" (BYOK) package.</span><span class="sxs-lookup"><span data-stu-id="77a06-218">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="77a06-219">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span><span class="sxs-lookup"><span data-stu-id="77a06-219">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="77a06-220">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="77a06-220">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="77a06-221">Delete the key vault and associated keys and secrets</span><span class="sxs-lookup"><span data-stu-id="77a06-221">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="77a06-222">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the `az keyvault delete` command:</span><span class="sxs-lookup"><span data-stu-id="77a06-222">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="77a06-223">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span><span class="sxs-lookup"><span data-stu-id="77a06-223">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="77a06-224">Other Azure Cross-Platform Command-line Interface Commands</span><span class="sxs-lookup"><span data-stu-id="77a06-224">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="77a06-225">Other commands that you might useful for managing Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="77a06-225">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="77a06-226">This command lists a tabular display of all keys and selected properties:</span><span class="sxs-lookup"><span data-stu-id="77a06-226">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="77a06-227">az keyvault key list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="77a06-227">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="77a06-228">This command displays a full list of properties for the specified key:</span><span class="sxs-lookup"><span data-stu-id="77a06-228">This command displays a full list of properties for the specified key:</span></span>

<span data-ttu-id="77a06-229">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="77a06-229">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="77a06-230">This command lists a tabular display of all secret names and selected properties:</span><span class="sxs-lookup"><span data-stu-id="77a06-230">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="77a06-231">az keyvault secret list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="77a06-231">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="77a06-232">Here's an example of how to remove a specific key:</span><span class="sxs-lookup"><span data-stu-id="77a06-232">Here's an example of how to remove a specific key:</span></span>

<span data-ttu-id="77a06-233">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="77a06-233">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="77a06-234">Here's an example of how to remove a specific secret:</span><span class="sxs-lookup"><span data-stu-id="77a06-234">Here's an example of how to remove a specific secret:</span></span>

<span data-ttu-id="77a06-235">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span><span class="sxs-lookup"><span data-stu-id="77a06-235">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="77a06-236">Next steps</span><span class="sxs-lookup"><span data-stu-id="77a06-236">Next steps</span></span>
<span data-ttu-id="77a06-237">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span><span class="sxs-lookup"><span data-stu-id="77a06-237">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="77a06-238">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="77a06-238">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
