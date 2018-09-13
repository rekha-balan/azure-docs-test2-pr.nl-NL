---
title: Azure CLI Script Sample - Create a web app and deploy code from a local Git repository | Microsoft Docs
description: Azure CLI Script Sample - Create a web app and deploy code from a local Git repository
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 048f98aa-f708-44cb-9b9e-953f67dc6da8
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 12/11/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: af779677bd43e78b80224c8033f873fac6fdd54e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855922"
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="f4a47-103">Create a web app and deploy code from a local Git repository</span><span class="sxs-lookup"><span data-stu-id="f4a47-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="f4a47-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span><span class="sxs-lookup"><span data-stu-id="f4a47-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f4a47-105">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="f4a47-105">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f4a47-106">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="f4a47-106">To find the version, run `az --version`.</span></span> <span data-ttu-id="f4a47-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f4a47-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="sample-script"></a><span data-ttu-id="f4a47-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="f4a47-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f4a47-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="f4a47-109">Script explanation</span></span>

<span data-ttu-id="f4a47-110">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="f4a47-110">This script uses the following commands.</span></span> <span data-ttu-id="f4a47-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="f4a47-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f4a47-112">Command</span><span class="sxs-lookup"><span data-stu-id="f4a47-112">Command</span></span> | <span data-ttu-id="f4a47-113">Notes</span><span class="sxs-lookup"><span data-stu-id="f4a47-113">Notes</span></span> |
|---|---|
| [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) | <span data-ttu-id="f4a47-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="f4a47-114">Creates a resource group in which all resources are stored.</span></span> |
| [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) | <span data-ttu-id="f4a47-115">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="f4a47-115">Creates an App Service plan.</span></span> |
| [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) | <span data-ttu-id="f4a47-116">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="f4a47-116">Creates an Azure web app.</span></span> |
| [`az webapp deployment user set`](/cli/azure/webapp/deployment/user?view=azure-cli-latest#az-webapp-deployment-user-set) | <span data-ttu-id="f4a47-117">Sets the account-level deployment credentials for App Service.</span><span class="sxs-lookup"><span data-stu-id="f4a47-117">Sets the account-level deployment credentials for App Service.</span></span> |
| [`az webapp deployment source config-local-git`](/cli/azure/webapp/deployment/source?view=azure-cli-latest#az-webapp-deployment-source-config-local-git) | <span data-ttu-id="f4a47-118">Creates a source control configuration for a local Git repository.</span><span class="sxs-lookup"><span data-stu-id="f4a47-118">Creates a source control configuration for a local Git repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f4a47-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="f4a47-119">Next steps</span></span>

<span data-ttu-id="f4a47-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="f4a47-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="f4a47-121">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f4a47-121">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
