---
title: Azure CLI Script Sample - Create a Function App for serverless execution | Microsoft Docs
description: Azure CLI Script Sample - Create a Function App for serverless execution
services: functions
documentationcenter: functions
author: ggailey777
manager: jeconnoc
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: azure-functions
ms.devlang: azurecli
ms.topic: sample
ms.date: 07/03/2018
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 55cb9d318c06ed3ecef87ab457c7405aecbf1238
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968140"
---
# <a name="create-a-function-app-for-serverless-code-execution"></a><span data-ttu-id="f45be-103">Create a function app for serverless code execution</span><span class="sxs-lookup"><span data-stu-id="f45be-103">Create a function app for serverless code execution</span></span>

<span data-ttu-id="f45be-104">This Azure Functions sample script creates a function app, which is a container for your functions.</span><span class="sxs-lookup"><span data-stu-id="f45be-104">This Azure Functions sample script creates a function app, which is a container for your functions.</span></span> <span data-ttu-id="f45be-105">The function app is created using the [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span><span class="sxs-lookup"><span data-stu-id="f45be-105">The function app is created using the [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span></span>

[!INCLUDE [upgrade runtime](../../../includes/functions-cli-version-note.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f45be-106">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="f45be-106">If you choose to install and use the CLI locally, this article requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f45be-107">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="f45be-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="f45be-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f45be-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f45be-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="f45be-109">Sample script</span></span>

<span data-ttu-id="f45be-110">This script creates an Azure Function app using the [consumption plan](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="f45be-110">This script creates an Azure Function app using the [consumption plan](../functions-scale.md#consumption-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f45be-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="f45be-111">Script explanation</span></span>

<span data-ttu-id="f45be-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="f45be-112">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="f45be-113">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="f45be-113">This script uses the following commands:</span></span>

| <span data-ttu-id="f45be-114">Command</span><span class="sxs-lookup"><span data-stu-id="f45be-114">Command</span></span> | <span data-ttu-id="f45be-115">Notes</span><span class="sxs-lookup"><span data-stu-id="f45be-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f45be-116">az group create</span><span class="sxs-lookup"><span data-stu-id="f45be-116">az group create</span></span>](/cli/azure/group#az-group-create) | <span data-ttu-id="f45be-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="f45be-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f45be-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="f45be-118">az storage account create</span></span>](/cli/azure/storage/account#az-storage-account-create) | <span data-ttu-id="f45be-119">Creates an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="f45be-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="f45be-120">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="f45be-120">az functionapp create</span></span>](/cli/azure/functionapp#az-functionapp-create) | <span data-ttu-id="f45be-121">Creates a function app.</span><span class="sxs-lookup"><span data-stu-id="f45be-121">Creates a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f45be-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="f45be-122">Next steps</span></span>

<span data-ttu-id="f45be-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="f45be-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="f45be-124">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f45be-124">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
