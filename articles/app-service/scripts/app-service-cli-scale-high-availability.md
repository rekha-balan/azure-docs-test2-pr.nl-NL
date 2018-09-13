---
title: Azure CLI Script Sample - Scale a web app worldwide with a high-availabilty architecture | Microsoft Docs
description: Azure CLI Script Sample - Scale a web app worldwide with a high-availabilty architecture
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: e4033a50-0e05-4505-8ce8-c876204b2acc
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 12/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 825dcce494c24c931544363f8f2edb6935560ae1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871057"
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="a5efb-103">Scale a web app worldwide with a high-availability architecture</span><span class="sxs-lookup"><span data-stu-id="a5efb-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="a5efb-104">This sample script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span><span class="sxs-lookup"><span data-stu-id="a5efb-104">This sample script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="a5efb-105">Once the exercise is complete, you have a high-available architecture, which provides global availability of your web app based on the lowest network latency.</span><span class="sxs-lookup"><span data-stu-id="a5efb-105">Once the exercise is complete, you have a high-available architecture, which provides global availability of your web app based on the lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a5efb-106">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="a5efb-106">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a5efb-107">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="a5efb-107">To find the version, run `az --version`.</span></span> <span data-ttu-id="a5efb-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a5efb-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="sample-script"></a><span data-ttu-id="a5efb-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="a5efb-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a5efb-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="a5efb-110">Script explanation</span></span>

<span data-ttu-id="a5efb-111">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="a5efb-111">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="a5efb-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="a5efb-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a5efb-113">Command</span><span class="sxs-lookup"><span data-stu-id="a5efb-113">Command</span></span> | <span data-ttu-id="a5efb-114">Notes</span><span class="sxs-lookup"><span data-stu-id="a5efb-114">Notes</span></span> |
|---|---|
| [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) | <span data-ttu-id="a5efb-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="a5efb-115">Creates a resource group in which all resources are stored.</span></span> |
| [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) | <span data-ttu-id="a5efb-116">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="a5efb-116">Creates an App Service plan.</span></span> |
| [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) | <span data-ttu-id="a5efb-117">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="a5efb-117">Creates an Azure web app.</span></span> |
| [`az network traffic-manager profile create`](/cli/azure/network/traffic-manager/profile?view=azure-cli-latest#az-network-traffic-manager-profile-create) | <span data-ttu-id="a5efb-118">Creates an Azure Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="a5efb-118">Creates an Azure Traffic Manager profile.</span></span> |
| [`az network traffic-manager endpoint create`](/cli/azure/network/traffic-manager/endpoint?view=azure-cli-latest#az-network-traffic-manager-endpoint-create) | <span data-ttu-id="a5efb-119">Adds an endpoint to an Azure Traffic Manager Profile.</span><span class="sxs-lookup"><span data-stu-id="a5efb-119">Adds an endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a5efb-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="a5efb-120">Next steps</span></span>

<span data-ttu-id="a5efb-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="a5efb-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="a5efb-122">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a5efb-122">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
