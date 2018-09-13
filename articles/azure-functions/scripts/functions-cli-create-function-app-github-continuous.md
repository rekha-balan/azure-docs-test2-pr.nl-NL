---
title: Create a function in Azure that is deployed from GitHub | Microsoft Docs
description: Create a function app and deploy function code from a GitHub repository using Azure Functions.
services: functions
ms.service: azure-functions
keywords: ''
ms.devlang: azurecli
author: ggailey777
ms.author: glenga
ms.date: 07/03/2018
ms.topic: sample
ms.custom: mvc
ms.openlocfilehash: f2d2eb20f3b609fce164bc1cbd33162b5afbe6c8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866540"
---
# <a name="create-a-function-app-in-azure-that-is-deployed-from-github"></a><span data-ttu-id="eca38-103">Create a function app in Azure that is deployed from GitHub</span><span class="sxs-lookup"><span data-stu-id="eca38-103">Create a function app in Azure that is deployed from GitHub</span></span>

<span data-ttu-id="eca38-104">This Azure Functions sample script creates a function app using the [consumption plan](../functions-scale.md#consumption-plan), along with its related resources.</span><span class="sxs-lookup"><span data-stu-id="eca38-104">This Azure Functions sample script creates a function app using the [consumption plan](../functions-scale.md#consumption-plan), along with its related resources.</span></span> <span data-ttu-id="eca38-105">The script also configures your function code for  continuous deployment from a GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="eca38-105">The script also configures your function code for  continuous deployment from a GitHub repository.</span></span> 

[!INCLUDE [upgrade runtime](../../../includes/functions-cli-version-note.md)]

<span data-ttu-id="eca38-106">In this sample, you need:</span><span class="sxs-lookup"><span data-stu-id="eca38-106">In this sample, you need:</span></span>

* <span data-ttu-id="eca38-107">A GitHub repository with functions code, that you have administrative permissions for.</span><span class="sxs-lookup"><span data-stu-id="eca38-107">A GitHub repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="eca38-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span><span class="sxs-lookup"><span data-stu-id="eca38-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="eca38-109">If you rather use the Azure CLI locally, you must install and use version 2.0 or a later version.</span><span class="sxs-lookup"><span data-stu-id="eca38-109">If you rather use the Azure CLI locally, you must install and use version 2.0 or a later version.</span></span> <span data-ttu-id="eca38-110">To determine the Azure CLI version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="eca38-110">To determine the Azure CLI version, run `az --version`.</span></span> <span data-ttu-id="eca38-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eca38-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="eca38-112">Sample script</span><span class="sxs-lookup"><span data-stu-id="eca38-112">Sample script</span></span>

<span data-ttu-id="eca38-113">This sample creates an Azure Function app and deploys function code from GitHub.</span><span class="sxs-lookup"><span data-stu-id="eca38-113">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="eca38-114">Script explanation</span><span class="sxs-lookup"><span data-stu-id="eca38-114">Script explanation</span></span>

<span data-ttu-id="eca38-115">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="eca38-115">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="eca38-116">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="eca38-116">This script uses the following commands:</span></span>

| <span data-ttu-id="eca38-117">Command</span><span class="sxs-lookup"><span data-stu-id="eca38-117">Command</span></span> | <span data-ttu-id="eca38-118">Notes</span><span class="sxs-lookup"><span data-stu-id="eca38-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="eca38-119">az group create</span><span class="sxs-lookup"><span data-stu-id="eca38-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-create) | <span data-ttu-id="eca38-120">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="eca38-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="eca38-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="eca38-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#az-storage-account-create) | <span data-ttu-id="eca38-122">Creates the storage account required by the function app.</span><span class="sxs-lookup"><span data-stu-id="eca38-122">Creates the storage account required by the function app.</span></span> |
| [<span data-ttu-id="eca38-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="eca38-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#az-functionapp-create) | <span data-ttu-id="eca38-124">Creates a function app in the serverless [consumption plan](../functions-scale.md#consumption-plan) and associates it with a Git or Mercurial repository.</span><span class="sxs-lookup"><span data-stu-id="eca38-124">Creates a function app in the serverless [consumption plan](../functions-scale.md#consumption-plan) and associates it with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="eca38-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="eca38-125">Next steps</span></span>

<span data-ttu-id="eca38-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="eca38-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="eca38-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="eca38-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
