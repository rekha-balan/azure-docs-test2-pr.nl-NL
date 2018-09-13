---
title: Azure CLI Script Sample - Create a web app and deploy files with FTP | Microsoft Docs
description: Azure CLI Script Sample - Create a web app and deploy files with FTP
services: app-service\web
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
tags: azure-service-management
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: sample
ms.topic: sample
ms.date: 12/12/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 8be2bc575649febe7870129b5b4c9996d7de0728
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870171"
---
# <a name="create-a-web-app-and-deploy-files-with-ftp"></a><span data-ttu-id="50a12-103">Create a web app and deploy files with FTP</span><span class="sxs-lookup"><span data-stu-id="50a12-103">Create a web app and deploy files with FTP</span></span>

<span data-ttu-id="50a12-104">This sample script creates a web app in App Service with its related resources, and then deploys a static HTML page using FTP.</span><span class="sxs-lookup"><span data-stu-id="50a12-104">This sample script creates a web app in App Service with its related resources, and then deploys a static HTML page using FTP.</span></span> <span data-ttu-id="50a12-105">For FTP upload, the script uses [cURL](https://en.wikipedia.org/wiki/CURL) as an example.</span><span class="sxs-lookup"><span data-stu-id="50a12-105">For FTP upload, the script uses [cURL](https://en.wikipedia.org/wiki/CURL) as an example.</span></span> <span data-ttu-id="50a12-106">You can use whatever FTP tool to upload your files.</span><span class="sxs-lookup"><span data-stu-id="50a12-106">You can use whatever FTP tool to upload your files.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="50a12-107">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="50a12-107">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="50a12-108">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="50a12-108">To find the version, run `az --version`.</span></span> <span data-ttu-id="50a12-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="50a12-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="sample-script"></a><span data-ttu-id="50a12-110">Sample script</span><span class="sxs-lookup"><span data-stu-id="50a12-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-ftp/deploy-ftp.sh "Create a web app and deploy files with FTP")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="50a12-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="50a12-111">Script explanation</span></span> 

<span data-ttu-id="50a12-112">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="50a12-112">This script uses the following commands.</span></span> <span data-ttu-id="50a12-113">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="50a12-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="50a12-114">Command</span><span class="sxs-lookup"><span data-stu-id="50a12-114">Command</span></span> | <span data-ttu-id="50a12-115">Notes</span><span class="sxs-lookup"><span data-stu-id="50a12-115">Notes</span></span> |
|---|---|
| [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) | <span data-ttu-id="50a12-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="50a12-116">Creates a resource group in which all resources are stored.</span></span> |
| [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) | <span data-ttu-id="50a12-117">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="50a12-117">Creates an App Service plan.</span></span> |
| [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) | <span data-ttu-id="50a12-118">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="50a12-118">Creates an Azure web app.</span></span> |
| [`az webapp deployment list-publishing-profiles`](/cli/azure/webapp/deployment?view=azure-cli-latest#az-webapp-deployment-list-publishing-profiles) | <span data-ttu-id="50a12-119">Get the details for available web app deployment profiles.</span><span class="sxs-lookup"><span data-stu-id="50a12-119">Get the details for available web app deployment profiles.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="50a12-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="50a12-120">Next steps</span></span>

<span data-ttu-id="50a12-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="50a12-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="50a12-122">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="50a12-122">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
