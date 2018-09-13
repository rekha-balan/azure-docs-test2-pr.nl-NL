---
title: Azure Quickstart - Set and retrieve a secret from Key Vault using Azure CLI | Microsoft Docs
description: Quickstart showing how to set and retrieve a secret from Azure Key Vault using Azure CLI
services: key-vault
author: barclayn
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 4acc894f-fee0-4c2f-988e-bc0eceea5eda
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.custom: mvc
ms.date: 05/10/2018
ms.author: barclayn
ms.openlocfilehash: ad5a8e1443b1dd125a4572676aa5666b7fb2746f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968627"
---
# <a name="quickstart-set-and-retrieve-a-secret-from-azure-key-vault-using-azure-cli"></a><span data-ttu-id="ae8a8-103">Quickstart: Set and retrieve a secret from Azure Key Vault using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ae8a8-103">Quickstart: Set and retrieve a secret from Azure Key Vault using Azure CLI</span></span>

<span data-ttu-id="ae8a8-104">Azure Key Vault is a cloud service that works as a secure secrets store.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-104">Azure Key Vault is a cloud service that works as a secure secrets store.</span></span> <span data-ttu-id="ae8a8-105">You can securely store keys, passwords, certificates and other secrets.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-105">You can securely store keys, passwords, certificates and other secrets.</span></span> <span data-ttu-id="ae8a8-106">For more information on Key Vault you may review the [Overview](key-vault-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ae8a8-106">For more information on Key Vault you may review the [Overview](key-vault-overview.md).</span></span> <span data-ttu-id="ae8a8-107">Azure CLI is used to create and manage Azure resources using commands or scripts.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-107">Azure CLI is used to create and manage Azure resources using commands or scripts.</span></span> <span data-ttu-id="ae8a8-108">In this quickstart, you create a key vault.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-108">In this quickstart, you create a key vault.</span></span> <span data-ttu-id="ae8a8-109">Once that you have completed that, you will store a secret.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-109">Once that you have completed that, you will store a secret.</span></span>

<span data-ttu-id="ae8a8-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ae8a8-111">If you choose to install and use the CLI locally, this quickstart requires the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-111">If you choose to install and use the CLI locally, this quickstart requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ae8a8-112">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="ae8a8-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ae8a8-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="ae8a8-114">To log in to the Azure using the CLI you can type:</span><span class="sxs-lookup"><span data-stu-id="ae8a8-114">To log in to the Azure using the CLI you can type:</span></span>

```azurecli
az login
```

<span data-ttu-id="ae8a8-115">For more information on login options via the CLI take a look at [Log in with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli?view=azure-cli-latest)</span><span class="sxs-lookup"><span data-stu-id="ae8a8-115">For more information on login options via the CLI take a look at [Log in with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli?view=azure-cli-latest)</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="ae8a8-116">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="ae8a8-116">Create a resource group</span></span>

<span data-ttu-id="ae8a8-117">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="ae8a8-118">The following example creates a resource group named *ContosoResourceGroup* in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-118">The following example creates a resource group named *ContosoResourceGroup* in the *eastus* location.</span></span>

```azurecli
az group create --name 'ContosoResourceGroup' --location eastus
```

## <a name="create-a-key-vault"></a><span data-ttu-id="ae8a8-119">Create a Key Vault</span><span class="sxs-lookup"><span data-stu-id="ae8a8-119">Create a Key Vault</span></span>

<span data-ttu-id="ae8a8-120">Next you will create a Key Vault in the resource group created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-120">Next you will create a Key Vault in the resource group created in the previous step.</span></span> <span data-ttu-id="ae8a8-121">You will need to provide some information:</span><span class="sxs-lookup"><span data-stu-id="ae8a8-121">You will need to provide some information:</span></span>

- <span data-ttu-id="ae8a8-122">For this quickstart we use **Contoso-vault2**.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-122">For this quickstart we use **Contoso-vault2**.</span></span> <span data-ttu-id="ae8a8-123">You must provide a unique name in your testing.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-123">You must provide a unique name in your testing.</span></span>
- <span data-ttu-id="ae8a8-124">Resource group name **ContosoResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-124">Resource group name **ContosoResourceGroup**.</span></span>
- <span data-ttu-id="ae8a8-125">The location **East US**.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-125">The location **East US**.</span></span>

```azurecli
az keyvault create --name 'Contoso-Vault2' --resource-group 'ContosoResourceGroup' --location eastus
```

<span data-ttu-id="ae8a8-126">The output of this cmdlet shows properties of the newly created Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-126">The output of this cmdlet shows properties of the newly created Key Vault.</span></span> <span data-ttu-id="ae8a8-127">Take note of the two properties listed below:</span><span class="sxs-lookup"><span data-stu-id="ae8a8-127">Take note of the two properties listed below:</span></span>

- <span data-ttu-id="ae8a8-128">**Vault Name**: In the example, this is **Contoso-Vault2**.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-128">**Vault Name**: In the example, this is **Contoso-Vault2**.</span></span> <span data-ttu-id="ae8a8-129">You will use this name for other Key Vault commands.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-129">You will use this name for other Key Vault commands.</span></span>
- <span data-ttu-id="ae8a8-130">**Vault URI**: In the example, this is https://contoso-vault2.vault.azure.net/.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-130">**Vault URI**: In the example, this is https://contoso-vault2.vault.azure.net/.</span></span> <span data-ttu-id="ae8a8-131">Applications that use your vault through its REST API must use this URI.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-131">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="ae8a8-132">At this point, your Azure account is the only one authorized to perform any operations on this new vault.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-132">At this point, your Azure account is the only one authorized to perform any operations on this new vault.</span></span>

## <a name="add-a-secret-to-key-vault"></a><span data-ttu-id="ae8a8-133">Add a secret to Key Vault</span><span class="sxs-lookup"><span data-stu-id="ae8a8-133">Add a secret to Key Vault</span></span>

<span data-ttu-id="ae8a8-134">To add a secret to the vault, you just need to take a couple of additional steps.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-134">To add a secret to the vault, you just need to take a couple of additional steps.</span></span> <span data-ttu-id="ae8a8-135">This password could be used by an application.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-135">This password could be used by an application.</span></span> <span data-ttu-id="ae8a8-136">The password will be called **ExamplePassword** and will store the value of **Pa$$w0rd** in it.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-136">The password will be called **ExamplePassword** and will store the value of **Pa$$w0rd** in it.</span></span>

<span data-ttu-id="ae8a8-137">Type the commands below to create a secret in Key Vault called **ExamplePassword** that will store the value **Pa$$w0rd** :</span><span class="sxs-lookup"><span data-stu-id="ae8a8-137">Type the commands below to create a secret in Key Vault called **ExamplePassword** that will store the value **Pa$$w0rd** :</span></span>

```azurecli
az keyvault secret set --vault-name 'Contoso-Vault2' --name 'ExamplePassword' --value 'Pa$$w0rd'
```

<span data-ttu-id="ae8a8-138">You can now reference this password that you added to Azure Key Vault by using its URI.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-138">You can now reference this password that you added to Azure Key Vault by using its URI.</span></span> <span data-ttu-id="ae8a8-139">Use **https://ContosoVault.vault.azure.net/secrets/ExamplePassword** to get the current version.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-139">Use **https://ContosoVault.vault.azure.net/secrets/ExamplePassword** to get the current version.</span></span> 

<span data-ttu-id="ae8a8-140">To view the value contained in the secret as plain text:</span><span class="sxs-lookup"><span data-stu-id="ae8a8-140">To view the value contained in the secret as plain text:</span></span>

```azurecli
az keyvault secret show --name 'ExamplePassword' --vault-name 'Contoso-Vault2'
```

<span data-ttu-id="ae8a8-141">Now, you have created a Key Vault, stored a secret, and retrieved it.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-141">Now, you have created a Key Vault, stored a secret, and retrieved it.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="ae8a8-142">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="ae8a8-142">Clean up resources</span></span>

<span data-ttu-id="ae8a8-143">Other quickstarts and tutorials in this collection build upon this quickstart.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-143">Other quickstarts and tutorials in this collection build upon this quickstart.</span></span> <span data-ttu-id="ae8a8-144">If you plan to continue on to work with subsequent quickstarts and tutorials, you may wish to leave these resources in place.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-144">If you plan to continue on to work with subsequent quickstarts and tutorials, you may wish to leave these resources in place.</span></span>
<span data-ttu-id="ae8a8-145">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-145">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, and all related resources.</span></span> <span data-ttu-id="ae8a8-146">You can delete the resources as follows:</span><span class="sxs-lookup"><span data-stu-id="ae8a8-146">You can delete the resources as follows:</span></span>

```azurecli
az group delete --name ContosoResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="ae8a8-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="ae8a8-147">Next steps</span></span>

<span data-ttu-id="ae8a8-148">In this quickstart, you have created a Key Vault and stored a secret in it.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-148">In this quickstart, you have created a Key Vault and stored a secret in it.</span></span> <span data-ttu-id="ae8a8-149">To learn more about Key Vault and how you can use it with your applications continue to the tutorial for web applications working with Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ae8a8-149">To learn more about Key Vault and how you can use it with your applications continue to the tutorial for web applications working with Key Vault.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="ae8a8-150">To learn how to read a secret from Key Vault from a web application using managed identities for Azure resources, continue with the following tutorial [Configure an Azure web application to read a secret from Key vault](quick-create-net.md)</span><span class="sxs-lookup"><span data-stu-id="ae8a8-150">To learn how to read a secret from Key Vault from a web application using managed identities for Azure resources, continue with the following tutorial [Configure an Azure web application to read a secret from Key vault](quick-create-net.md)</span></span>
