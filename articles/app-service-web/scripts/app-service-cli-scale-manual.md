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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.openlocfilehash: 2023e806d8ed5dc459af93533db6668659ba5898
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553432"
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="146f4-103">Scale a web app manually</span><span class="sxs-lookup"><span data-stu-id="146f4-103">Scale a web app manually</span></span>

<span data-ttu-id="146f4-104">In this scenario you will learn to create a resource group, app service plan and web app.</span><span class="sxs-lookup"><span data-stu-id="146f4-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="146f4-105">You will then scale the App Service Plan from a single instance to multiple instances.</span><span class="sxs-lookup"><span data-stu-id="146f4-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="146f4-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="146f4-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="146f4-107">Script explanation</span><span class="sxs-lookup"><span data-stu-id="146f4-107">Script explanation</span></span>

<span data-ttu-id="146f4-108">This script uses the following commands to create a resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="146f4-108">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="146f4-109">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="146f4-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="146f4-110">Command</span><span class="sxs-lookup"><span data-stu-id="146f4-110">Command</span></span> | <span data-ttu-id="146f4-111">Notes</span><span class="sxs-lookup"><span data-stu-id="146f4-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="146f4-112">az group create</span><span class="sxs-lookup"><span data-stu-id="146f4-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="146f4-113">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="146f4-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="146f4-114">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="146f4-114">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="146f4-115">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="146f4-115">Creates an App Service plan.</span></span> <span data-ttu-id="146f4-116">This is like a server farm for your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="146f4-116">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="146f4-117">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="146f4-117">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="146f4-118">Creates an Azure web app within the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="146f4-118">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="146f4-119">az appservice plan update</span><span class="sxs-lookup"><span data-stu-id="146f4-119">az appservice plan update</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#update) | <span data-ttu-id="146f4-120">Updates properties of the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="146f4-120">Updates properties of the App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="146f4-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="146f4-121">Next steps</span></span>

<span data-ttu-id="146f4-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="146f4-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="146f4-123">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="146f4-123">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>