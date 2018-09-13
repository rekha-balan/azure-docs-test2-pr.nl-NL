---
title: Azure CLI Script Sample - Map a custom domain to a web app | Microsoft Docs
description: Azure CLI Script Sample - Map a custom domain to a web app
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 5ac4a680-cc73-4578-bcd6-8668c08802c2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 04/09/2017
ms.author: cephalin
ms.openlocfilehash: 480c18285e4708ce2771f10a848e4a55acf0c817
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551305"
---
# <a name="map-a-custom-domain-to-a-web-app"></a><span data-ttu-id="ded47-103">Map a custom domain to a web app</span><span class="sxs-lookup"><span data-stu-id="ded47-103">Map a custom domain to a web app</span></span>

<span data-ttu-id="ded47-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` to it.</span><span class="sxs-lookup"><span data-stu-id="ded47-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` to it.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="ded47-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="ded47-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain to a web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ded47-106">Script explanation</span><span class="sxs-lookup"><span data-stu-id="ded47-106">Script explanation</span></span>

<span data-ttu-id="ded47-107">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="ded47-107">This script uses the following commands.</span></span> <span data-ttu-id="ded47-108">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="ded47-108">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ded47-109">Command</span><span class="sxs-lookup"><span data-stu-id="ded47-109">Command</span></span> | <span data-ttu-id="ded47-110">Notes</span><span class="sxs-lookup"><span data-stu-id="ded47-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ded47-111">az group create</span><span class="sxs-lookup"><span data-stu-id="ded47-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ded47-112">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="ded47-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ded47-113">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="ded47-113">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="ded47-114">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="ded47-114">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="ded47-115">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="ded47-115">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="ded47-116">Creates a web app.</span><span class="sxs-lookup"><span data-stu-id="ded47-116">Creates a web app.</span></span> |
| [<span data-ttu-id="ded47-117">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="ded47-117">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="ded47-118">Map a custom domain to a web app.</span><span class="sxs-lookup"><span data-stu-id="ded47-118">Map a custom domain to a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ded47-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="ded47-119">Next steps</span></span>

<span data-ttu-id="ded47-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ded47-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ded47-121">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ded47-121">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
