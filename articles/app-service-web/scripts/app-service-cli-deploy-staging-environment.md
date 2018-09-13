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
ms.topic: article
ms.date: 03/20/2017
ms.author: cephalin
ms.openlocfilehash: 184b099e0b723016180adaef95dc092da4d4224c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555044"
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a><span data-ttu-id="61d69-103">Create a web app and deploy code to a staging environment</span><span class="sxs-lookup"><span data-stu-id="61d69-103">Create a web app and deploy code to a staging environment</span></span>

<span data-ttu-id="61d69-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span><span class="sxs-lookup"><span data-stu-id="61d69-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="61d69-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="61d69-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Create a web app and deploy code to a staging environment")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="61d69-106">Script explanation</span><span class="sxs-lookup"><span data-stu-id="61d69-106">Script explanation</span></span>

<span data-ttu-id="61d69-107">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="61d69-107">This script uses the following commands.</span></span> <span data-ttu-id="61d69-108">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="61d69-108">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="61d69-109">Command</span><span class="sxs-lookup"><span data-stu-id="61d69-109">Command</span></span> | <span data-ttu-id="61d69-110">Notes</span><span class="sxs-lookup"><span data-stu-id="61d69-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="61d69-111">az group create</span><span class="sxs-lookup"><span data-stu-id="61d69-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="61d69-112">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="61d69-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="61d69-113">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="61d69-113">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="61d69-114">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="61d69-114">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="61d69-115">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="61d69-115">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="61d69-116">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="61d69-116">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="61d69-117">az appservice web deployment slot create</span><span class="sxs-lookup"><span data-stu-id="61d69-117">az appservice web deployment slot create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/deployment/slot#create) | <span data-ttu-id="61d69-118">Create a deployment slot.</span><span class="sxs-lookup"><span data-stu-id="61d69-118">Create a deployment slot.</span></span> |
| [<span data-ttu-id="61d69-119">az appservice web source-control config</span><span class="sxs-lookup"><span data-stu-id="61d69-119">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="61d69-120">Associates an Azure web app with a Git or Mercurial repository.</span><span class="sxs-lookup"><span data-stu-id="61d69-120">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="61d69-121">az appservice web browse</span><span class="sxs-lookup"><span data-stu-id="61d69-121">az appservice web browse</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#browse) | <span data-ttu-id="61d69-122">Open an Azure web app in a browser.</span><span class="sxs-lookup"><span data-stu-id="61d69-122">Open an Azure web app in a browser.</span></span> |
| [<span data-ttu-id="61d69-123">az appservice web deployment slot swap</span><span class="sxs-lookup"><span data-stu-id="61d69-123">az appservice web deployment slot swap</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/deployment/slot#swap) | <span data-ttu-id="61d69-124">Swap a specified deployment slot into production.</span><span class="sxs-lookup"><span data-stu-id="61d69-124">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="61d69-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="61d69-125">Next steps</span></span>

<span data-ttu-id="61d69-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="61d69-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="61d69-127">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="61d69-127">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>