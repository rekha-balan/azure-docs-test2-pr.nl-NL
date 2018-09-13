---
title: Azure CLI Script Sample - Create a Batch account | Microsoft Docs
description: Azure CLI Script Sample - Create a Batch account
services: batch
documentationcenter: ''
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: ''
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/20/2017
ms.author: antisch
ms.openlocfilehash: e4ff70c2e741f0f0de693a2997501a446f84bf0a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555213"
---
# <a name="create-a-batch-account-with-the-azure-cli"></a><span data-ttu-id="f5217-103">Create a Batch account with the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f5217-103">Create a Batch account with the Azure CLI</span></span>

<span data-ttu-id="f5217-104">This script creates an Azure Batch account and shows how various properties of the account can be queried and updated.</span><span class="sxs-lookup"><span data-stu-id="f5217-104">This script creates an Azure Batch account and shows how various properties of the account can be queried and updated.</span></span>

<span data-ttu-id="f5217-105">If needed, install the Azure CLI using the instructions found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to log into Azure.</span><span class="sxs-lookup"><span data-stu-id="f5217-105">If needed, install the Azure CLI using the instructions found in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), and then run `az login` to log into Azure.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="f5217-106">Batch account sample script</span><span class="sxs-lookup"><span data-stu-id="f5217-106">Batch account sample script</span></span>

<span data-ttu-id="f5217-107">When you create a Batch account, by default its compute nodes are assigned internally by the Batch service.</span><span class="sxs-lookup"><span data-stu-id="f5217-107">When you create a Batch account, by default its compute nodes are assigned internally by the Batch service.</span></span> <span data-ttu-id="f5217-108">Allocated compute nodes will be subject to a separate core quota and the account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span><span class="sxs-lookup"><span data-stu-id="f5217-108">Allocated compute nodes will be subject to a separate core quota and the account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="f5217-109">Batch account using user subscription sample script</span><span class="sxs-lookup"><span data-stu-id="f5217-109">Batch account using user subscription sample script</span></span>

<span data-ttu-id="f5217-110">You can also opt to have Batch create its compute nodes in your own Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f5217-110">You can also opt to have Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="f5217-111">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and the compute nodes allocated will count towards your subscription quota.</span><span class="sxs-lookup"><span data-stu-id="f5217-111">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and the compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="f5217-112">To create an account in this mode, one must specify a Key Vault reference when creating the account.</span><span class="sxs-lookup"><span data-stu-id="f5217-112">To create an account in this mode, one must specify a Key Vault reference when creating the account.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f5217-113">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="f5217-113">Clean up deployment</span></span>

<span data-ttu-id="f5217-114">After you run either of the above sample scripts, run the following command to remove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span><span class="sxs-lookup"><span data-stu-id="f5217-114">After you run either of the above sample scripts, run the following command to remove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f5217-115">Script explanation</span><span class="sxs-lookup"><span data-stu-id="f5217-115">Script explanation</span></span>

<span data-ttu-id="f5217-116">This script uses the following commands to create a resource group, Batch account, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="f5217-116">This script uses the following commands to create a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="f5217-117">Each command in the table links to command-specific documentation.</span><span class="sxs-lookup"><span data-stu-id="f5217-117">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="f5217-118">Command</span><span class="sxs-lookup"><span data-stu-id="f5217-118">Command</span></span> | <span data-ttu-id="f5217-119">Notes</span><span class="sxs-lookup"><span data-stu-id="f5217-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f5217-120">az group create</span><span class="sxs-lookup"><span data-stu-id="f5217-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f5217-121">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="f5217-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f5217-122">az batch account create</span><span class="sxs-lookup"><span data-stu-id="f5217-122">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="f5217-123">Creates the Batch account.</span><span class="sxs-lookup"><span data-stu-id="f5217-123">Creates the Batch account.</span></span>  |
| [<span data-ttu-id="f5217-124">az batch account set</span><span class="sxs-lookup"><span data-stu-id="f5217-124">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="f5217-125">Updates properties of the Batch account.</span><span class="sxs-lookup"><span data-stu-id="f5217-125">Updates properties of the Batch account.</span></span>  |
| [<span data-ttu-id="f5217-126">az batch account show</span><span class="sxs-lookup"><span data-stu-id="f5217-126">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="f5217-127">Retrieves details of the specified Batch account.</span><span class="sxs-lookup"><span data-stu-id="f5217-127">Retrieves details of the specified Batch account.</span></span>  |
| [<span data-ttu-id="f5217-128">az batch account keys list</span><span class="sxs-lookup"><span data-stu-id="f5217-128">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="f5217-129">Retrieves the access keys of the specified Batch account.</span><span class="sxs-lookup"><span data-stu-id="f5217-129">Retrieves the access keys of the specified Batch account.</span></span>  |
| [<span data-ttu-id="f5217-130">az batch account login</span><span class="sxs-lookup"><span data-stu-id="f5217-130">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="f5217-131">Authenticates against the specified Batch account for further CLI interaction.</span><span class="sxs-lookup"><span data-stu-id="f5217-131">Authenticates against the specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="f5217-132">az storage account create</span><span class="sxs-lookup"><span data-stu-id="f5217-132">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="f5217-133">Creates a storage account.</span><span class="sxs-lookup"><span data-stu-id="f5217-133">Creates a storage account.</span></span> |
| [<span data-ttu-id="f5217-134">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="f5217-134">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="f5217-135">Creates a key vault.</span><span class="sxs-lookup"><span data-stu-id="f5217-135">Creates a key vault.</span></span> |
| [<span data-ttu-id="f5217-136">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="f5217-136">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="f5217-137">Update the security policy of the specified key vault.</span><span class="sxs-lookup"><span data-stu-id="f5217-137">Update the security policy of the specified key vault.</span></span> |
| [<span data-ttu-id="f5217-138">az group delete</span><span class="sxs-lookup"><span data-stu-id="f5217-138">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="f5217-139">Deletes a resource group including all nested resources.</span><span class="sxs-lookup"><span data-stu-id="f5217-139">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f5217-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="f5217-140">Next steps</span></span>

<span data-ttu-id="f5217-141">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f5217-141">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f5217-142">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f5217-142">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
