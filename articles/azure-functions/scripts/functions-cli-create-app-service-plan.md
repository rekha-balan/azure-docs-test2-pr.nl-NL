---
title: Azure CLI Script Sample - Create a Function App in an App Service plan | Microsoft Docs
description: Azure CLI Script Sample - Create a Function App in an App Service plan
services: functions
documentationcenter: functions
author: ggailey777
manager: jeconnoc
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: azure-functions
ms.devlang: azurecli
ms.topic: sample
ms.date: 07/03/2018
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 5462ba4006253862b9505c77a67c7b9e468ed9ab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868417"
---
# <a name="create-a-function-app-in-an-app-service-plan"></a><span data-ttu-id="ef641-103">Create a Function App in an App Service plan</span><span class="sxs-lookup"><span data-stu-id="ef641-103">Create a Function App in an App Service plan</span></span>

<span data-ttu-id="ef641-104">This Azure Functions sample script creates a function app, which is a container for your functions.</span><span class="sxs-lookup"><span data-stu-id="ef641-104">This Azure Functions sample script creates a function app, which is a container for your functions.</span></span> <span data-ttu-id="ef641-105">The function app that is created uses a dedicated App Service plan, which means your server resources are always on.</span><span class="sxs-lookup"><span data-stu-id="ef641-105">The function app that is created uses a dedicated App Service plan, which means your server resources are always on.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ef641-106">If you choose to install and use the CLI locally, this article requires the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="ef641-106">If you choose to install and use the CLI locally, this article requires the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ef641-107">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="ef641-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="ef641-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ef641-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ef641-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="ef641-109">Sample script</span></span>

<span data-ttu-id="ef641-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="ef641-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ef641-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="ef641-111">Script explanation</span></span>

<span data-ttu-id="ef641-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="ef641-112">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="ef641-113">This script uses the following commands:</span><span class="sxs-lookup"><span data-stu-id="ef641-113">This script uses the following commands:</span></span>

| <span data-ttu-id="ef641-114">Command</span><span class="sxs-lookup"><span data-stu-id="ef641-114">Command</span></span> | <span data-ttu-id="ef641-115">Notes</span><span class="sxs-lookup"><span data-stu-id="ef641-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ef641-116">az group create</span><span class="sxs-lookup"><span data-stu-id="ef641-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-create) | <span data-ttu-id="ef641-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="ef641-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ef641-118">az storage account create</span><span class="sxs-lookup"><span data-stu-id="ef641-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#az-storage-account-create) | <span data-ttu-id="ef641-119">Creates an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="ef641-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="ef641-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="ef641-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#az-appservice-plan-create) | <span data-ttu-id="ef641-121">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="ef641-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="ef641-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="ef641-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#az-functionapp-create) | <span data-ttu-id="ef641-123">Creates a function app in the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="ef641-123">Creates a function app in the App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ef641-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="ef641-124">Next steps</span></span>

<span data-ttu-id="ef641-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="ef641-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="ef641-126">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ef641-126">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
