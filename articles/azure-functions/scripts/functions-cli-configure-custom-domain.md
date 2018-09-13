---
title: Azure CLI Script Sample - Map a custom domain to a function app | Microsoft Docs
description: Azure CLI Script Sample - Map a custom domain to a function app in Azure.
services: functions
documentationcenter: ''
author: ggailey777
manager: jeconnoc
ms.assetid: d127e347-7581-47d7-b289-e0f51f2fbfbc
ms.service: azure-functions
ms.devlang: azurecli
ms.topic: sample
ms.date: 07/04/2018
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c5ae5ef52d60fd96a9398835b109475c08549f52
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857902"
---
# <a name="map-a-custom-domain-to-a-function-app"></a><span data-ttu-id="c85d2-103">Map a custom domain to a function app</span><span class="sxs-lookup"><span data-stu-id="c85d2-103">Map a custom domain to a function app</span></span>

<span data-ttu-id="c85d2-104">This sample script creates a function app in an App Service plan and then maps it to a custom domain that you provide.</span><span class="sxs-lookup"><span data-stu-id="c85d2-104">This sample script creates a function app in an App Service plan and then maps it to a custom domain that you provide.</span></span> <span data-ttu-id="c85d2-105">When your function app is hosted in an [App Service plan](../functions-scale.md#app-service-plan), you can map a custom domain using either a CNAME or an A record.</span><span class="sxs-lookup"><span data-stu-id="c85d2-105">When your function app is hosted in an [App Service plan](../functions-scale.md#app-service-plan), you can map a custom domain using either a CNAME or an A record.</span></span> <span data-ttu-id="c85d2-106">For function apps in a [Consumption plan](../functions-scale.md#consumption-plan), only the CNAME option is supported.</span><span class="sxs-lookup"><span data-stu-id="c85d2-106">For function apps in a [Consumption plan](../functions-scale.md#consumption-plan), only the CNAME option is supported.</span></span> <span data-ttu-id="c85d2-107">This sample creates an App Service plan and requires an A record to map the domain.</span><span class="sxs-lookup"><span data-stu-id="c85d2-107">This sample creates an App Service plan and requires an A record to map the domain.</span></span> 

<span data-ttu-id="c85d2-108">To run this sample script, you must have already configured an A record in your custom domain that points to your web app's default domain name.</span><span class="sxs-lookup"><span data-stu-id="c85d2-108">To run this sample script, you must have already configured an A record in your custom domain that points to your web app's default domain name.</span></span> <span data-ttu-id="c85d2-109">For more information, see the [Map custom domain instructions for Azure App Service](https://aka.ms/appservicecustomdns).</span><span class="sxs-lookup"><span data-stu-id="c85d2-109">For more information, see the [Map custom domain instructions for Azure App Service](https://aka.ms/appservicecustomdns).</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c85d2-110">If you choose to install and use the CLI locally, you must use the Azure CLI version 2.0 or a later version.</span><span class="sxs-lookup"><span data-stu-id="c85d2-110">If you choose to install and use the CLI locally, you must use the Azure CLI version 2.0 or a later version.</span></span> <span data-ttu-id="c85d2-111">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="c85d2-111">To find the version, run `az --version`.</span></span> <span data-ttu-id="c85d2-112">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c85d2-112">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="c85d2-113">Sample script</span><span class="sxs-lookup"><span data-stu-id="c85d2-113">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain to a function app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c85d2-114">Script explanation</span><span class="sxs-lookup"><span data-stu-id="c85d2-114">Script explanation</span></span>

<span data-ttu-id="c85d2-115">This script uses the following commands: Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="c85d2-115">This script uses the following commands: Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c85d2-116">Command</span><span class="sxs-lookup"><span data-stu-id="c85d2-116">Command</span></span> | <span data-ttu-id="c85d2-117">Notes</span><span class="sxs-lookup"><span data-stu-id="c85d2-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c85d2-118">az group create</span><span class="sxs-lookup"><span data-stu-id="c85d2-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-create) | <span data-ttu-id="c85d2-119">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="c85d2-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c85d2-120">az storage account create</span><span class="sxs-lookup"><span data-stu-id="c85d2-120">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#az-storage-account-create) | <span data-ttu-id="c85d2-121">Creates a storage account required by the function app.</span><span class="sxs-lookup"><span data-stu-id="c85d2-121">Creates a storage account required by the function app.</span></span> |
| [<span data-ttu-id="c85d2-122">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="c85d2-122">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#az-appservice-plan-create) | <span data-ttu-id="c85d2-123">Creates an App Service plan required to map a custom domain.</span><span class="sxs-lookup"><span data-stu-id="c85d2-123">Creates an App Service plan required to map a custom domain.</span></span> |
| [<span data-ttu-id="c85d2-124">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="c85d2-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#az-functionapp-create) | <span data-ttu-id="c85d2-125">Creates a function app in the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="c85d2-125">Creates a function app in the App Service plan.</span></span> |
| [<span data-ttu-id="c85d2-126">az functionapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="c85d2-126">az functionapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/functionapp/config/hostname#az-functionapp-config-hostname-add) | <span data-ttu-id="c85d2-127">Maps a custom domain to a function app.</span><span class="sxs-lookup"><span data-stu-id="c85d2-127">Maps a custom domain to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c85d2-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="c85d2-128">Next steps</span></span>

<span data-ttu-id="c85d2-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="c85d2-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="c85d2-130">Additional Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c85d2-130">Additional Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
