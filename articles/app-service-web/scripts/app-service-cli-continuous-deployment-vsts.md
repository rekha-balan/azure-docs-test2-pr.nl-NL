---
title: Azure CLI Script Sample - Create a web app with continuous deployment from Visual Studio Team Services | Microsoft Docs
description: Azure CLI Script Sample - Create a web app with continuous deployment from Visual Studio Team Services
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
ms.topic: article
ms.date: 03/20/2017
ms.author: cfowler
ms.openlocfilehash: b82e51d8d96c98cba1d5989060eed40ed7f2d4fe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564609"
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="e9864-103">Create a web app with continuous deployment from Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="e9864-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="e9864-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span><span class="sxs-lookup"><span data-stu-id="e9864-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="e9864-105">For this sample, you will need:</span><span class="sxs-lookup"><span data-stu-id="e9864-105">For this sample, you will need:</span></span>

* <span data-ttu-id="e9864-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span><span class="sxs-lookup"><span data-stu-id="e9864-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="e9864-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span><span class="sxs-lookup"><span data-stu-id="e9864-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="create-app-sample"></a><span data-ttu-id="e9864-108">Create app sample</span><span class="sxs-lookup"><span data-stu-id="e9864-108">Create app sample</span></span>

[!code-azurecli[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e9864-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="e9864-109">Script explanation</span></span>

<span data-ttu-id="e9864-110">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="e9864-110">This script uses the following commands.</span></span> <span data-ttu-id="e9864-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="e9864-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e9864-112">Command</span><span class="sxs-lookup"><span data-stu-id="e9864-112">Command</span></span> | <span data-ttu-id="e9864-113">Notes</span><span class="sxs-lookup"><span data-stu-id="e9864-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e9864-114">az group create</span><span class="sxs-lookup"><span data-stu-id="e9864-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e9864-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="e9864-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e9864-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="e9864-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="e9864-117">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="e9864-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="e9864-118">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="e9864-118">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="e9864-119">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="e9864-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="e9864-120">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="e9864-120">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="e9864-121">Associates an Azure web app with a Git or Mercurial repository.</span><span class="sxs-lookup"><span data-stu-id="e9864-121">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="e9864-122">az appservice web browse</span><span class="sxs-lookup"><span data-stu-id="e9864-122">az appservice web browse</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#browse) | <span data-ttu-id="e9864-123">Open an Azure web app in a browser.</span><span class="sxs-lookup"><span data-stu-id="e9864-123">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e9864-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="e9864-124">Next steps</span></span>

<span data-ttu-id="e9864-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e9864-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e9864-126">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e9864-126">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>