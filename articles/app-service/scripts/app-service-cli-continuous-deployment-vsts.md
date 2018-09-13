---
title: Azure CLI Script Sample - Create a web app with continuous deployment from Azure DevOps Services | Microsoft Docs
description: Azure CLI Script Sample - Create a web app with continuous deployment from Azure DevOps Services
services: app-service\web
documentationcenter: ''
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 389d3bd3-cd8e-4715-a3a1-031ec061d385
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 12/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 0c73d502455261c74215054a86fbb67907404e76
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868313"
---
# <a name="create-a-web-app-with-continuous-deployment-from-azure-devops"></a><span data-ttu-id="d5acb-103">Create a web app with continuous deployment from Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="d5acb-103">Create a web app with continuous deployment from Azure DevOps</span></span>

<span data-ttu-id="d5acb-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Azure DevOps repository.</span><span class="sxs-lookup"><span data-stu-id="d5acb-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Azure DevOps repository.</span></span> <span data-ttu-id="d5acb-105">For this sample, you need:</span><span class="sxs-lookup"><span data-stu-id="d5acb-105">For this sample, you need:</span></span>

* <span data-ttu-id="d5acb-106">A Azure DevOps repository with application code, that you have administrative permissions for.</span><span class="sxs-lookup"><span data-stu-id="d5acb-106">A Azure DevOps repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="d5acb-107">A [Personal Access Token (PAT)](https://docs.microsoft.com/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=vsts) for your Azure DevOps organization.</span><span class="sxs-lookup"><span data-stu-id="d5acb-107">A [Personal Access Token (PAT)](https://docs.microsoft.com/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=vsts) for your Azure DevOps organization.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d5acb-108">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="d5acb-108">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d5acb-109">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="d5acb-109">To find the version, run `az --version`.</span></span> <span data-ttu-id="d5acb-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d5acb-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="sample-script"></a><span data-ttu-id="d5acb-111">Sample script</span><span class="sxs-lookup"><span data-stu-id="d5acb-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Azure DevOps")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="d5acb-112">Script explanation</span><span class="sxs-lookup"><span data-stu-id="d5acb-112">Script explanation</span></span>

<span data-ttu-id="d5acb-113">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="d5acb-113">This script uses the following commands.</span></span> <span data-ttu-id="d5acb-114">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="d5acb-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d5acb-115">Command</span><span class="sxs-lookup"><span data-stu-id="d5acb-115">Command</span></span> | <span data-ttu-id="d5acb-116">Notes</span><span class="sxs-lookup"><span data-stu-id="d5acb-116">Notes</span></span> |
|---|---|
| [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) | <span data-ttu-id="d5acb-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="d5acb-117">Creates a resource group in which all resources are stored.</span></span> |
| [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) | <span data-ttu-id="d5acb-118">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="d5acb-118">Creates an App Service plan.</span></span> |
| [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) | <span data-ttu-id="d5acb-119">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="d5acb-119">Creates an Azure web app.</span></span> |
| [`az webapp deployment source config`](/cli/azure/webapp/deployment/source?view=azure-cli-latest#az-webapp-deployment-source-config) | <span data-ttu-id="d5acb-120">Associates an Azure web app with a Git or Mercurial repository.</span><span class="sxs-lookup"><span data-stu-id="d5acb-120">Associates an Azure web app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d5acb-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="d5acb-121">Next steps</span></span>

<span data-ttu-id="d5acb-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="d5acb-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="d5acb-123">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d5acb-123">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
