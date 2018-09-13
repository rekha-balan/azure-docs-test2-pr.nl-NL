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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.openlocfilehash: 4e74b414103fb39fca001ee3629bf004653cb7a3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564592"
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container"></a><span data-ttu-id="7a7b6-103">Create an ASP.NET Core web app in a Docker container</span><span class="sxs-lookup"><span data-stu-id="7a7b6-103">Create an ASP.NET Core web app in a Docker container</span></span>

<span data-ttu-id="7a7b6-104">In this scenario you will learn how to create a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container.</span><span class="sxs-lookup"><span data-stu-id="7a7b6-104">In this scenario you will learn how to create a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="7a7b6-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="7a7b6-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Linux Docker")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="7a7b6-106">Script explanation</span><span class="sxs-lookup"><span data-stu-id="7a7b6-106">Script explanation</span></span>

<span data-ttu-id="7a7b6-107">This script uses the following commands to create a resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="7a7b6-107">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="7a7b6-108">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="7a7b6-108">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7a7b6-109">Command</span><span class="sxs-lookup"><span data-stu-id="7a7b6-109">Command</span></span> | <span data-ttu-id="7a7b6-110">Notes</span><span class="sxs-lookup"><span data-stu-id="7a7b6-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7a7b6-111">az group create</span><span class="sxs-lookup"><span data-stu-id="7a7b6-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7a7b6-112">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="7a7b6-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7a7b6-113">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="7a7b6-113">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="7a7b6-114">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="7a7b6-114">Creates an App Service plan.</span></span> <span data-ttu-id="7a7b6-115">This is like a server farm for your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="7a7b6-115">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="7a7b6-116">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="7a7b6-116">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="7a7b6-117">Creates an Azure web app within the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="7a7b6-117">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="7a7b6-118">az appservice web config container update</span><span class="sxs-lookup"><span data-stu-id="7a7b6-118">az appservice web config container update</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/container#update) | <span data-ttu-id="7a7b6-119">Sets the Docker container for the Azure web app.</span><span class="sxs-lookup"><span data-stu-id="7a7b6-119">Sets the Docker container for the Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7a7b6-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="7a7b6-120">Next steps</span></span>

<span data-ttu-id="7a7b6-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7a7b6-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7a7b6-122">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7a7b6-122">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>