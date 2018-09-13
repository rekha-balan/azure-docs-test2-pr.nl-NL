---
title: Azure CLI Script Sample - Create a web app and deploy code from a local Git repository | Microsoft Docs
description: Azure CLI Script Sample - Create a web app and deploy code from a local Git repository
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 048f98aa-f708-44cb-9b9e-953f67dc6da8
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cephalin
ms.openlocfilehash: 76e82a217f3a48dc57f3a6e88507f89ed1936eaf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669043"
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="3f098-103">Create a web app and deploy code from a local Git repository</span><span class="sxs-lookup"><span data-stu-id="3f098-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="3f098-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span><span class="sxs-lookup"><span data-stu-id="3f098-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="3f098-105">Sample script</span><span class="sxs-lookup"><span data-stu-id="3f098-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="3f098-106">Script explanation</span><span class="sxs-lookup"><span data-stu-id="3f098-106">Script explanation</span></span>

<span data-ttu-id="3f098-107">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="3f098-107">This script uses the following commands.</span></span> <span data-ttu-id="3f098-108">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="3f098-108">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3f098-109">Command</span><span class="sxs-lookup"><span data-stu-id="3f098-109">Command</span></span> | <span data-ttu-id="3f098-110">Notes</span><span class="sxs-lookup"><span data-stu-id="3f098-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3f098-111">az group create</span><span class="sxs-lookup"><span data-stu-id="3f098-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3f098-112">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="3f098-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3f098-113">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="3f098-113">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="3f098-114">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="3f098-114">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="3f098-115">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="3f098-115">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="3f098-116">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="3f098-116">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="3f098-117">az appservice web deployment user set</span><span class="sxs-lookup"><span data-stu-id="3f098-117">az appservice web deployment user set</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/deployment/user#set) | <span data-ttu-id="3f098-118">Sets the account-level deployment credentials for App Service.</span><span class="sxs-lookup"><span data-stu-id="3f098-118">Sets the account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="3f098-119">az appservice web source-control config-local-git</span><span class="sxs-lookup"><span data-stu-id="3f098-119">az appservice web source-control config-local-git</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config-local-git) | <span data-ttu-id="3f098-120">Creates a source control configuration for a local Git repository.</span><span class="sxs-lookup"><span data-stu-id="3f098-120">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="3f098-121">az appservice web browse</span><span class="sxs-lookup"><span data-stu-id="3f098-121">az appservice web browse</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#browse) | <span data-ttu-id="3f098-122">Open an Azure web app in a browser.</span><span class="sxs-lookup"><span data-stu-id="3f098-122">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3f098-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="3f098-123">Next steps</span></span>

<span data-ttu-id="3f098-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3f098-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3f098-125">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3f098-125">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>