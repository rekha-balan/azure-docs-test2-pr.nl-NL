---
title: Azure CLI Script Sample - Create a web app and deploy code to a staging environment | Microsoft Docs
description: Azure CLI Script Sample - Create a web app and deploy code to a staging environment
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 2b995dcd-e471-4355-9fda-00babcdb156e
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 12/11/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 36cd7656eea91c5be009395087239219942b1204
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857162"
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a><span data-ttu-id="c4fc0-103">Create a web app and deploy code to a staging environment</span><span class="sxs-lookup"><span data-stu-id="c4fc0-103">Create a web app and deploy code to a staging environment</span></span>

<span data-ttu-id="c4fc0-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span><span class="sxs-lookup"><span data-stu-id="c4fc0-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c4fc0-105">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="c4fc0-105">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c4fc0-106">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="c4fc0-106">To find the version, run `az --version`.</span></span> <span data-ttu-id="c4fc0-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c4fc0-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="sample-script"></a><span data-ttu-id="c4fc0-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="c4fc0-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Create a web app and deploy code to a staging environment")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c4fc0-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="c4fc0-109">Script explanation</span></span>

<span data-ttu-id="c4fc0-110">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="c4fc0-110">This script uses the following commands.</span></span> <span data-ttu-id="c4fc0-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="c4fc0-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c4fc0-112">Command</span><span class="sxs-lookup"><span data-stu-id="c4fc0-112">Command</span></span> | <span data-ttu-id="c4fc0-113">Notes</span><span class="sxs-lookup"><span data-stu-id="c4fc0-113">Notes</span></span> |
|---|---|
| [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) | <span data-ttu-id="c4fc0-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="c4fc0-114">Creates a resource group in which all resources are stored.</span></span> |
| [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) | <span data-ttu-id="c4fc0-115">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="c4fc0-115">Creates an App Service plan.</span></span> |
| [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) | <span data-ttu-id="c4fc0-116">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="c4fc0-116">Creates an Azure web app.</span></span> |
| [`az webapp deployment slot create`](/cli/azure/webapp/deployment/slot?view=azure-cli-latest#az-webapp-deployment-slot-create) | <span data-ttu-id="c4fc0-117">Create a deployment slot.</span><span class="sxs-lookup"><span data-stu-id="c4fc0-117">Create a deployment slot.</span></span> |
| [`az webapp deployment source config`](/cli/azure/webapp/deployment/source?view=azure-cli-latest#az-webapp-deployment-source-config) | <span data-ttu-id="c4fc0-118">Associates an Azure web app with a Git or Mercurial repository.</span><span class="sxs-lookup"><span data-stu-id="c4fc0-118">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [`az webapp deployment slot swap`](/cli/azure/webapp/deployment/slot?view=azure-cli-latest#az-webapp-deployment-slot-swap) | <span data-ttu-id="c4fc0-119">Swap a specified deployment slot into production.</span><span class="sxs-lookup"><span data-stu-id="c4fc0-119">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c4fc0-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="c4fc0-120">Next steps</span></span>

<span data-ttu-id="c4fc0-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="c4fc0-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="c4fc0-122">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c4fc0-122">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
