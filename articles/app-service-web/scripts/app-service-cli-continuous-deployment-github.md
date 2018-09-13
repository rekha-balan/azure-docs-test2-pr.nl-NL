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
ms.topic: article
ms.date: 03/20/2017
ms.author: cephalin
ms.openlocfilehash: 44eaabecf9b53f2552d1dff3502139520a611ccd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552507"
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="c67bb-103">Create a web app with continuous deployment from GitHub</span><span class="sxs-lookup"><span data-stu-id="c67bb-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="c67bb-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="c67bb-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="c67bb-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="c67bb-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="c67bb-106">In this sample, you will need:</span><span class="sxs-lookup"><span data-stu-id="c67bb-106">In this sample, you will need:</span></span>

* <span data-ttu-id="c67bb-107">A GitHub repository with application code, that you have administrative permissions for.</span><span class="sxs-lookup"><span data-stu-id="c67bb-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="c67bb-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span><span class="sxs-lookup"><span data-stu-id="c67bb-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="create-app-sample"></a><span data-ttu-id="c67bb-109">Create app sample</span><span class="sxs-lookup"><span data-stu-id="c67bb-109">Create app sample</span></span>

[!code-azurecli[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c67bb-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="c67bb-110">Script explanation</span></span>

<span data-ttu-id="c67bb-111">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="c67bb-111">This script uses the following commands.</span></span> <span data-ttu-id="c67bb-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="c67bb-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c67bb-113">Command</span><span class="sxs-lookup"><span data-stu-id="c67bb-113">Command</span></span> | <span data-ttu-id="c67bb-114">Notes</span><span class="sxs-lookup"><span data-stu-id="c67bb-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c67bb-115">az group create</span><span class="sxs-lookup"><span data-stu-id="c67bb-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c67bb-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="c67bb-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c67bb-117">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="c67bb-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="c67bb-118">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="c67bb-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c67bb-119">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="c67bb-119">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="c67bb-120">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="c67bb-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="c67bb-121">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="c67bb-121">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="c67bb-122">Associates an Azure web app with a Git or Mercurial repository.</span><span class="sxs-lookup"><span data-stu-id="c67bb-122">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="c67bb-123">az appservice web browse</span><span class="sxs-lookup"><span data-stu-id="c67bb-123">az appservice web browse</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#browse) | <span data-ttu-id="c67bb-124">Open an Azure web app in a browser.</span><span class="sxs-lookup"><span data-stu-id="c67bb-124">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c67bb-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="c67bb-125">Next steps</span></span>

<span data-ttu-id="c67bb-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c67bb-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c67bb-127">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c67bb-127">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>