---
title: Create an Azure Function that connects to an Azure Storage | Microsoft Docs
description: Azure CLI Script Sample - Create an Azure Function that connects to an Azure Storage
services: functions
documentationcenter: functions
author: ggailey777
manager: jeconnoc
ms.assetid: ''
ms.service: azure-functions
ms.devlang: azurecli
ms.topic: sample
ms.date: 04/20/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: aa25c0e636c36422cb6b576d0ca8ebc899b2a2dc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857317"
---
# <a name="create-a-function-app-that-connects-to-an-azure-storage-account"></a><span data-ttu-id="01980-103">Create a function app that connects to an Azure Storage account</span><span class="sxs-lookup"><span data-stu-id="01980-103">Create a function app that connects to an Azure Storage account</span></span>

<span data-ttu-id="01980-104">This Azure Functions sample script creates a function app and connects the function to an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="01980-104">This Azure Functions sample script creates a function app and connects the function to an Azure Storage account.</span></span> <span data-ttu-id="01980-105">The created app setting that contains the connection can be used with a [storage trigger or binding](..\functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="01980-105">The created app setting that contains the connection can be used with a [storage trigger or binding](..\functions-bindings-storage-blob.md).</span></span> 

[!INCLUDE [upgrade runtime](../../../includes/functions-cli-version-note.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="01980-106">If you use the CLI locally, make sure that you are running the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="01980-106">If you use the CLI locally, make sure that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="01980-107">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="01980-107">To find the version, run `az --version`.</span></span> <span data-ttu-id="01980-108">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="01980-108">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="01980-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="01980-109">Sample script</span></span>

<span data-ttu-id="01980-110">This sample creates an Azure Function app and adds the storage connection string to an app setting.</span><span class="sxs-lookup"><span data-stu-id="01980-110">This sample creates an Azure Function app and adds the storage connection string to an app setting.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]


## <a name="clean-up-deployment"></a><span data-ttu-id="01980-111">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="01980-111">Clean up deployment</span></span>

<span data-ttu-id="01980-112">After the script sample has been run, run the following command to remove the resource group and all related resources:</span><span class="sxs-lookup"><span data-stu-id="01980-112">After the script sample has been run, run the following command to remove the resource group and all related resources:</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="01980-113">Script explanation</span><span class="sxs-lookup"><span data-stu-id="01980-113">Script explanation</span></span>

<span data-ttu-id="01980-114">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="01980-114">This script uses the following commands.</span></span> <span data-ttu-id="01980-115">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="01980-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="01980-116">Command</span><span class="sxs-lookup"><span data-stu-id="01980-116">Command</span></span> | <span data-ttu-id="01980-117">Notes</span><span class="sxs-lookup"><span data-stu-id="01980-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="01980-118">az group create</span><span class="sxs-lookup"><span data-stu-id="01980-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-create) | <span data-ttu-id="01980-119">Create a resource group with location.</span><span class="sxs-lookup"><span data-stu-id="01980-119">Create a resource group with location.</span></span> |
| [<span data-ttu-id="01980-120">az storage account create</span><span class="sxs-lookup"><span data-stu-id="01980-120">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#az-storage-account-create) | <span data-ttu-id="01980-121">Create a storage account.</span><span class="sxs-lookup"><span data-stu-id="01980-121">Create a storage account.</span></span> |
| [<span data-ttu-id="01980-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="01980-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#az-functionapp-create) | <span data-ttu-id="01980-123">Creates a function app in the serverless [consumption plan](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="01980-123">Creates a function app in the serverless [consumption plan](../functions-scale.md#consumption-plan).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="01980-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="01980-124">Next steps</span></span>

<span data-ttu-id="01980-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="01980-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="01980-126">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="01980-126">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
