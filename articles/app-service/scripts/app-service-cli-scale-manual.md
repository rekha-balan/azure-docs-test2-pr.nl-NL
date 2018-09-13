---
title: Azure CLI Script Sample - Scale a Web App manually using Azure CLI 2.0 | Microsoft Docs
description: Azure CLI Script Sample - Scale a Web App manually using Azure CLI 2.0
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 251d9074-8fff-4121-ad16-9eca9556ac96
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 12/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 844250dce567bac280ae3a9a688cc8e5bc5852c9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870910"
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="f5b5e-103">Scale a web app manually</span><span class="sxs-lookup"><span data-stu-id="f5b5e-103">Scale a web app manually</span></span>

<span data-ttu-id="f5b5e-104">This sample script creates a resource group, an App Service plan, and a web app.</span><span class="sxs-lookup"><span data-stu-id="f5b5e-104">This sample script creates a resource group, an App Service plan, and a web app.</span></span> <span data-ttu-id="f5b5e-105">It then scales the App Service plan from a single instance to multiple instances.</span><span class="sxs-lookup"><span data-stu-id="f5b5e-105">It then scales the App Service plan from a single instance to multiple instances.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f5b5e-106">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="f5b5e-106">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f5b5e-107">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="f5b5e-107">To find the version, run `az --version`.</span></span> <span data-ttu-id="f5b5e-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f5b5e-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="sample-script"></a><span data-ttu-id="f5b5e-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="f5b5e-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f5b5e-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="f5b5e-110">Script explanation</span></span>

<span data-ttu-id="f5b5e-111">This script uses the following commands to create a resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="f5b5e-111">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="f5b5e-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="f5b5e-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f5b5e-113">Command</span><span class="sxs-lookup"><span data-stu-id="f5b5e-113">Command</span></span> | <span data-ttu-id="f5b5e-114">Notes</span><span class="sxs-lookup"><span data-stu-id="f5b5e-114">Notes</span></span> |
|---|---|
| [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) | <span data-ttu-id="f5b5e-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="f5b5e-115">Creates a resource group in which all resources are stored.</span></span> |
| [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) | <span data-ttu-id="f5b5e-116">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="f5b5e-116">Creates an App Service plan.</span></span> |
| [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) | <span data-ttu-id="f5b5e-117">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="f5b5e-117">Creates an Azure web app.</span></span> |
| [`az appservice plan update`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-update) | <span data-ttu-id="f5b5e-118">Updates properties of the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="f5b5e-118">Updates properties of the App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f5b5e-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="f5b5e-119">Next steps</span></span>

<span data-ttu-id="f5b5e-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="f5b5e-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="f5b5e-121">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f5b5e-121">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
