---
title: Azure CLI Script Sample - Back up a web app | Microsoft Docs
description: Azure CLI Script Sample - Back up a web app
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
ms.date: 12/07/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 91bf4c7fce40a8e8c94299919e0bdc25c3d3487c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870908"
---
# <a name="back-up-a-web-app"></a><span data-ttu-id="9c307-103">Back up a web app</span><span class="sxs-lookup"><span data-stu-id="9c307-103">Back up a web app</span></span>

<span data-ttu-id="9c307-104">This sample script creates a web app in App Service with its related resources, and then creates a one-time backup for it.</span><span class="sxs-lookup"><span data-stu-id="9c307-104">This sample script creates a web app in App Service with its related resources, and then creates a one-time backup for it.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9c307-105">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="9c307-105">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9c307-106">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="9c307-106">To find the version, run `az --version`.</span></span> <span data-ttu-id="9c307-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9c307-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="sample-script"></a><span data-ttu-id="9c307-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="9c307-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/backup-onetime/backup-onetime.sh?highlight=3-7 "Back up a web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="9c307-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="9c307-109">Script explanation</span></span>

<span data-ttu-id="9c307-110">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="9c307-110">This script uses the following commands.</span></span> <span data-ttu-id="9c307-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="9c307-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9c307-112">Command</span><span class="sxs-lookup"><span data-stu-id="9c307-112">Command</span></span> | <span data-ttu-id="9c307-113">Notes</span><span class="sxs-lookup"><span data-stu-id="9c307-113">Notes</span></span> |
|---|---|
| [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) | <span data-ttu-id="9c307-114">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="9c307-114">Creates a resource group in which all resources are stored.</span></span> |
| [`az storage account create`](/cli/azure/storage/account?view=azure-cli-latest#az-storage-account-create) | <span data-ttu-id="9c307-115">Creates a storage account.</span><span class="sxs-lookup"><span data-stu-id="9c307-115">Creates a storage account.</span></span> |
| [`az storage container create`](/cli/azure/storage/container?view=azure-cli-latest#az-storage-container-create) | <span data-ttu-id="9c307-116">Creates an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="9c307-116">Creates an Azure storage container.</span></span> |
| [`az storage container generate-sas`](/cli/azure/storage/container?view=azure-cli-latest#az-storage-container-generate-sas) | <span data-ttu-id="9c307-117">Generates an SAS token for an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="9c307-117">Generates an SAS token for an Azure storage container.</span></span>  |
| [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) | <span data-ttu-id="9c307-118">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="9c307-118">Creates an App Service plan.</span></span> |
| [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) | <span data-ttu-id="9c307-119">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="9c307-119">Creates an Azure web app.</span></span> |
| [`az webapp config backup create`](/cli/azure/webapp/config/backup?view=azure-cli-latest#az-webapp-config-backup-create) | <span data-ttu-id="9c307-120">Creates a backup for a web app.</span><span class="sxs-lookup"><span data-stu-id="9c307-120">Creates a backup for a web app.</span></span> |
| [`az webapp config backup list`](/cli/azure/webapp/config/backup?view=azure-cli-latest#az-webapp-config-backup-list) | <span data-ttu-id="9c307-121">Gets a list of backups for a web app.</span><span class="sxs-lookup"><span data-stu-id="9c307-121">Gets a list of backups for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9c307-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="9c307-122">Next steps</span></span>

<span data-ttu-id="9c307-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="9c307-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="9c307-124">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9c307-124">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
