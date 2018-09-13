---
title: Azure CLI Script Sample - Create a web app with continuous deployment from GitHub | Microsoft Docs
description: Azure CLI Script Sample - Create a web app with continuous deployment from GitHub
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 0205c991-0989-4ca3-bb41-237dcc964460
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 12/11/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 31eb2107b4c9bf2a5ac6b56896648a71a5e0c59e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864926"
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="99383-103">Create a web app with continuous deployment from GitHub</span><span class="sxs-lookup"><span data-stu-id="99383-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="99383-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="99383-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="99383-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="99383-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="99383-106">For this sample, you need:</span><span class="sxs-lookup"><span data-stu-id="99383-106">For this sample, you need:</span></span>

* <span data-ttu-id="99383-107">A GitHub repository with application code, that you have administrative permissions for.</span><span class="sxs-lookup"><span data-stu-id="99383-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="99383-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span><span class="sxs-lookup"><span data-stu-id="99383-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="99383-109">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="99383-109">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="99383-110">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="99383-110">To find the version, run `az --version`.</span></span> <span data-ttu-id="99383-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="99383-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="sample-script"></a><span data-ttu-id="99383-112">Sample script</span><span class="sxs-lookup"><span data-stu-id="99383-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="99383-113">Script explanation</span><span class="sxs-lookup"><span data-stu-id="99383-113">Script explanation</span></span>

<span data-ttu-id="99383-114">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="99383-114">This script uses the following commands.</span></span> <span data-ttu-id="99383-115">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="99383-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="99383-116">Command</span><span class="sxs-lookup"><span data-stu-id="99383-116">Command</span></span> | <span data-ttu-id="99383-117">Notes</span><span class="sxs-lookup"><span data-stu-id="99383-117">Notes</span></span> |
|---|---|
| [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) | <span data-ttu-id="99383-118">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="99383-118">Creates a resource group in which all resources are stored.</span></span> |
| [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) | <span data-ttu-id="99383-119">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="99383-119">Creates an App Service plan.</span></span> |
| [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) | <span data-ttu-id="99383-120">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="99383-120">Creates an Azure web app.</span></span> |
| [`az webapp deployment source config`](/cli/azure/webapp/deployment/source?view=azure-cli-latest#az-webapp-deployment-source-config) | <span data-ttu-id="99383-121">Associates an Azure web app with a Git or Mercurial repository.</span><span class="sxs-lookup"><span data-stu-id="99383-121">Associates an Azure web app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="99383-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="99383-122">Next steps</span></span>

<span data-ttu-id="99383-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="99383-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="99383-124">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="99383-124">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
