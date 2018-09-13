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
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cephalin
ms.openlocfilehash: 99fa912a47598801c4f8f3ad586319b89c14d73e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662187"
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="e6634-103">Create a web app with deployment from GitHub</span><span class="sxs-lookup"><span data-stu-id="e6634-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="e6634-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span><span class="sxs-lookup"><span data-stu-id="e6634-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="e6634-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="e6634-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="create-app-sample"></a><span data-ttu-id="e6634-106">Create app sample</span><span class="sxs-lookup"><span data-stu-id="e6634-106">Create app sample</span></span>

[!code-azurecli[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e6634-107">Script explanation</span><span class="sxs-lookup"><span data-stu-id="e6634-107">Script explanation</span></span>

<span data-ttu-id="e6634-108">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="e6634-108">This script uses the following commands.</span></span> <span data-ttu-id="e6634-109">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="e6634-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e6634-110">Command</span><span class="sxs-lookup"><span data-stu-id="e6634-110">Command</span></span> | <span data-ttu-id="e6634-111">Notes</span><span class="sxs-lookup"><span data-stu-id="e6634-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e6634-112">az group create</span><span class="sxs-lookup"><span data-stu-id="e6634-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e6634-113">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="e6634-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e6634-114">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="e6634-114">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="e6634-115">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="e6634-115">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="e6634-116">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="e6634-116">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="e6634-117">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="e6634-117">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="e6634-118">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="e6634-118">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="e6634-119">Associates an Azure web app with a Git or Mercurial repository.</span><span class="sxs-lookup"><span data-stu-id="e6634-119">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="e6634-120">az appservice web browse</span><span class="sxs-lookup"><span data-stu-id="e6634-120">az appservice web browse</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#browse) | <span data-ttu-id="e6634-121">Open an Azure web app in a browser.</span><span class="sxs-lookup"><span data-stu-id="e6634-121">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e6634-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="e6634-122">Next steps</span></span>

<span data-ttu-id="e6634-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e6634-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e6634-124">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e6634-124">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>