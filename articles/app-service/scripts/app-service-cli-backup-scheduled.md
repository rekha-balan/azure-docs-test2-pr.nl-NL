---
title: Azure CLI Script Sample - Create a scheduled backup for a web app | Microsoft Docs
description: Azure CLI Script Sample - Create a scheduled backup for a web app
services: app-service\web
documentationcenter: ''
author: cephalin
manager: cfowler
editor: ''
tags: azure-service-management
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 12/11/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 867adf4f2f669be00cb124625db2e14caa5179a2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867936"
---
# <a name="create-a-scheduled-backup-for-a-web-app"></a><span data-ttu-id="db9bb-103">Create a scheduled backup for a web app</span><span class="sxs-lookup"><span data-stu-id="db9bb-103">Create a scheduled backup for a web app</span></span>

<span data-ttu-id="db9bb-104">This sample script creates a web app in App Service with its related resources, and then creates a scheduled backup for it.</span><span class="sxs-lookup"><span data-stu-id="db9bb-104">This sample script creates a web app in App Service with its related resources, and then creates a scheduled backup for it.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="db9bb-105">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="db9bb-105">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="db9bb-106">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="db9bb-106">To find the version, run `az --version`.</span></span> <span data-ttu-id="db9bb-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="db9bb-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="db9bb-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="db9bb-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/backup-scheduled/backup-scheduled.sh?highlight=3-7 "Create a scheduled backup for a web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="db9bb-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="db9bb-109">Script explanation</span></span>

<span data-ttu-id="db9bb-110">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="db9bb-110">This script uses the following commands.</span></span> <span data-ttu-id="db9bb-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="db9bb-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="db9bb-112">Command</span><span class="sxs-lookup"><span data-stu-id="db9bb-112">Command</span></span> | <span data-ttu-id="db9bb-113">Notes</span><span class="sxs-lookup"><span data-stu-id="db9bb-113">Notes</span></span> |
|---|---|
| [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) | <span data-ttu-id="db9bb-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="db9bb-114">Creates a resource group in which all resources are stored.</span></span> |
| [`az storage account create`](/cli/azure/storage/account?view=azure-cli-latest#az-storage-account-create) | <span data-ttu-id="db9bb-115">Creates a storage account.</span><span class="sxs-lookup"><span data-stu-id="db9bb-115">Creates a storage account.</span></span> |
| [`az storage container create`](/cli/azure/storage/container?view=azure-cli-latest#az-storage-container-create) | <span data-ttu-id="db9bb-116">Creates an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="db9bb-116">Creates an Azure storage container.</span></span> |
| [`az storage container generate-sas`](/cli/azure/storage/container?view=azure-cli-latest#az-storage-container-generate-sas) | <span data-ttu-id="db9bb-117">Generates an SAS token for an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="db9bb-117">Generates an SAS token for an Azure storage container.</span></span>  |
| [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) | <span data-ttu-id="db9bb-118">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="db9bb-118">Creates an App Service plan.</span></span> |
| [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) | <span data-ttu-id="db9bb-119">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="db9bb-119">Creates an Azure web app.</span></span> |
| [`az webapp config backup update`](/cli/azure/webapp/config/backup?view=azure-cli-latest#az-webapp-config-backup-update) | <span data-ttu-id="db9bb-120">Configures a new backup schedule for a web app.</span><span class="sxs-lookup"><span data-stu-id="db9bb-120">Configures a new backup schedule for a web app.</span></span> |
| [`az webapp config backup show`](/cli/azure/webapp/config/backup?view=azure-cli-latest#az-webapp-config-backup-show) | <span data-ttu-id="db9bb-121">Shows the backup schedule for a web app.</span><span class="sxs-lookup"><span data-stu-id="db9bb-121">Shows the backup schedule for a web app.</span></span> |
| [`az webapp config backup list`](/cli/azure/webapp/config/backup?view=azure-cli-latest#az-webapp-config-backup-list) | <span data-ttu-id="db9bb-122">Gets a list of backups for a web app.</span><span class="sxs-lookup"><span data-stu-id="db9bb-122">Gets a list of backups for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="db9bb-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="db9bb-123">Next steps</span></span>

<span data-ttu-id="db9bb-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="db9bb-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="db9bb-125">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="db9bb-125">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
