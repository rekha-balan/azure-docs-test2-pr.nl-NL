---
title: Azure CLI Script Sample - Create a web app with deployment from GitHub | Microsoft Docs
description: Azure CLI Script Sample - Create a web app with deployment from GitHub
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
ms.tgt_pltfrm: sample
ms.topic: sample
ms.date: 12/11/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6cc4ae4a0b77aeb27c0fbde23dfd0dd65604ccf1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865411"
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="03e90-103">Create a web app with deployment from GitHub</span><span class="sxs-lookup"><span data-stu-id="03e90-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="03e90-104">This sample script creates a web app in App Service with its related resources.</span><span class="sxs-lookup"><span data-stu-id="03e90-104">This sample script creates a web app in App Service with its related resources.</span></span> <span data-ttu-id="03e90-105">It then deploys your web app code from a public GitHub repository (without continuous deployment).</span><span class="sxs-lookup"><span data-stu-id="03e90-105">It then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="03e90-106">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="03e90-106">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="03e90-107">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="03e90-107">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="03e90-108">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="03e90-108">To find the version, run `az --version`.</span></span> <span data-ttu-id="03e90-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="03e90-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="sample-script"></a><span data-ttu-id="03e90-110">Sample script</span><span class="sxs-lookup"><span data-stu-id="03e90-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="03e90-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="03e90-111">Script explanation</span></span> 

<span data-ttu-id="03e90-112">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="03e90-112">This script uses the following commands.</span></span> <span data-ttu-id="03e90-113">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="03e90-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="03e90-114">Command</span><span class="sxs-lookup"><span data-stu-id="03e90-114">Command</span></span> | <span data-ttu-id="03e90-115">Notes</span><span class="sxs-lookup"><span data-stu-id="03e90-115">Notes</span></span> |
|---|---|
| [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) | <span data-ttu-id="03e90-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="03e90-116">Creates a resource group in which all resources are stored.</span></span> |
| [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) | <span data-ttu-id="03e90-117">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="03e90-117">Creates an App Service plan.</span></span> |
| [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) | <span data-ttu-id="03e90-118">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="03e90-118">Creates an Azure web app.</span></span> |
| [`az webapp deployment source config`](/cli/azure/webapp/deployment/source?view=azure-cli-latest#az-webapp-deployment-source-config) | <span data-ttu-id="03e90-119">Associates an Azure web app with a Git or Mercurial repository.</span><span class="sxs-lookup"><span data-stu-id="03e90-119">Associates an Azure web app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="03e90-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="03e90-120">Next steps</span></span>

<span data-ttu-id="03e90-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="03e90-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="03e90-122">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="03e90-122">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
