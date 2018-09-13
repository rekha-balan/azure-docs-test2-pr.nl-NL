---
title: Create a function in Azure that is deployed from Azure DevOps | Microsoft Docs
description: Create a Function App and deploy function code from Azure DevOps
services: functions
keywords: ''
author: ggailey777
ms.author: glenga
ms.date: 07/03/2018
ms.topic: sample
ms.service: azure-functions
ms.custom: mvc
ms.openlocfilehash: f830cb02e62b3d794e880502260065098f3aff89
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857628"
---
# <a name="create-a-function-app-and-deploy-function-code-from-azure-devops"></a><span data-ttu-id="b62d2-103">Create a function app and deploy function code from Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="b62d2-103">Create a function app and deploy function code from Azure DevOps</span></span>

<span data-ttu-id="b62d2-104">This topic shows you how to use Azure Functions to create a [serverless](https://azure.microsoft.com/overview/serverless-computing/) function app using the [consumption plan](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="b62d2-104">This topic shows you how to use Azure Functions to create a [serverless](https://azure.microsoft.com/overview/serverless-computing/) function app using the [consumption plan](../functions-scale.md#consumption-plan).</span></span> <span data-ttu-id="b62d2-105">The function app, which is a container for your functions, is continuously deployed from a Azure DevOps repository.</span><span class="sxs-lookup"><span data-stu-id="b62d2-105">The function app, which is a container for your functions, is continuously deployed from a Azure DevOps repository.</span></span> 

[!INCLUDE [upgrade runtime](../../../includes/functions-cli-version-note.md)]

<span data-ttu-id="b62d2-106">To complete this topic, you must have:</span><span class="sxs-lookup"><span data-stu-id="b62d2-106">To complete this topic, you must have:</span></span>

* <span data-ttu-id="b62d2-107">An Azure DevOps repository that contains your function app project and to which you have administrative permissions.</span><span class="sxs-lookup"><span data-stu-id="b62d2-107">An Azure DevOps repository that contains your function app project and to which you have administrative permissions.</span></span>
* <span data-ttu-id="b62d2-108">A [personal access token (PAT)](https://docs.microsoft.com/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate) to access your Azure DevOps repository.</span><span class="sxs-lookup"><span data-stu-id="b62d2-108">A [personal access token (PAT)](https://docs.microsoft.com/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate) to access your Azure DevOps repository.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b62d2-109">If you rather use the Azure CLI locally, you must install and use version 2.0 or a later version.</span><span class="sxs-lookup"><span data-stu-id="b62d2-109">If you rather use the Azure CLI locally, you must install and use version 2.0 or a later version.</span></span> <span data-ttu-id="b62d2-110">To determine the Azure CLI version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="b62d2-110">To determine the Azure CLI version, run `az --version`.</span></span> <span data-ttu-id="b62d2-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b62d2-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b62d2-112">Sample script</span><span class="sxs-lookup"><span data-stu-id="b62d2-112">Sample script</span></span>

<span data-ttu-id="b62d2-113">This sample creates an Azure Function app and deploys function code from Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="b62d2-113">This sample creates an Azure Function app and deploys function code from Azure DevOps.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b62d2-114">Script explanation</span><span class="sxs-lookup"><span data-stu-id="b62d2-114">Script explanation</span></span>

<span data-ttu-id="b62d2-115">This script uses the following commands to create a resource group, storage account, function app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="b62d2-115">This script uses the following commands to create a resource group, storage account, function app, and all related resources.</span></span> <span data-ttu-id="b62d2-116">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="b62d2-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b62d2-117">Command</span><span class="sxs-lookup"><span data-stu-id="b62d2-117">Command</span></span> | <span data-ttu-id="b62d2-118">Notes</span><span class="sxs-lookup"><span data-stu-id="b62d2-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b62d2-119">az group create</span><span class="sxs-lookup"><span data-stu-id="b62d2-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-create) | <span data-ttu-id="b62d2-120">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="b62d2-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b62d2-121">az storage account create</span><span class="sxs-lookup"><span data-stu-id="b62d2-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#az-storage-account-create) | <span data-ttu-id="b62d2-122">Creates the storage account required by the function app.</span><span class="sxs-lookup"><span data-stu-id="b62d2-122">Creates the storage account required by the function app.</span></span> |
| [<span data-ttu-id="b62d2-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="b62d2-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#az-functionapp-create) | <span data-ttu-id="b62d2-124">Creates a function app in the serverless [consumption plan](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="b62d2-124">Creates a function app in the serverless [consumption plan](../functions-scale.md#consumption-plan).</span></span> |
| [<span data-ttu-id="b62d2-125">az functionapp deployment source config</span><span class="sxs-lookup"><span data-stu-id="b62d2-125">az functionapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/functionapp/deployment/source#az-functionapp-deployment-source-config) | <span data-ttu-id="b62d2-126">Associates a function app with a Git or Mercurial repository.</span><span class="sxs-lookup"><span data-stu-id="b62d2-126">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b62d2-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="b62d2-127">Next steps</span></span>

<span data-ttu-id="b62d2-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="b62d2-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="b62d2-129">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b62d2-129">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
