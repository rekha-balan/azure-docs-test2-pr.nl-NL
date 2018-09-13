---
title: Azure CLI Script Sample - Create an ASP.NET Core web app in a Docker container | Microsoft Docs
description: Azure CLI Script Sample - Create an ASP.NET Core web app in a Docker container
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 3a2d1983-ff7b-476a-ac44-49ec2aabb31a
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 12/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 2514617d2feca7ed349df42e27b0710a6b6c3a9b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867965"
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container"></a><span data-ttu-id="b5ab2-103">Create an ASP.NET Core web app in a Docker container</span><span class="sxs-lookup"><span data-stu-id="b5ab2-103">Create an ASP.NET Core web app in a Docker container</span></span>

<span data-ttu-id="b5ab2-104">This sample script creates a resource group, a Linux App Service plan, and a web app.</span><span class="sxs-lookup"><span data-stu-id="b5ab2-104">This sample script creates a resource group, a Linux App Service plan, and a web app.</span></span> <span data-ttu-id="b5ab2-105">It then deploys an ASP.NET Core application using a Docker Container.</span><span class="sxs-lookup"><span data-stu-id="b5ab2-105">It then deploys an ASP.NET Core application using a Docker Container.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b5ab2-106">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="b5ab2-106">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b5ab2-107">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="b5ab2-107">To find the version, run `az --version`.</span></span> <span data-ttu-id="b5ab2-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b5ab2-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="sample-script"></a><span data-ttu-id="b5ab2-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="b5ab2-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Linux Docker")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b5ab2-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="b5ab2-110">Script explanation</span></span>

<span data-ttu-id="b5ab2-111">This script uses the following commands to create a resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="b5ab2-111">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="b5ab2-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="b5ab2-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b5ab2-113">Command</span><span class="sxs-lookup"><span data-stu-id="b5ab2-113">Command</span></span> | <span data-ttu-id="b5ab2-114">Notes</span><span class="sxs-lookup"><span data-stu-id="b5ab2-114">Notes</span></span> |
|---|---|
| [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) | <span data-ttu-id="b5ab2-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="b5ab2-115">Creates a resource group in which all resources are stored.</span></span> |
| [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) | <span data-ttu-id="b5ab2-116">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="b5ab2-116">Creates an App Service plan.</span></span> |
| [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) | <span data-ttu-id="b5ab2-117">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="b5ab2-117">Creates an Azure web app.</span></span> |
| [`az webapp config container set`](/cli/azure/webapp/config/container?view=azure-cli-latest#az-webapp-config-container-set) | <span data-ttu-id="b5ab2-118">Sets the Docker container for the Azure web app.</span><span class="sxs-lookup"><span data-stu-id="b5ab2-118">Sets the Docker container for the Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b5ab2-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5ab2-119">Next steps</span></span>

<span data-ttu-id="b5ab2-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="b5ab2-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="b5ab2-121">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b5ab2-121">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
