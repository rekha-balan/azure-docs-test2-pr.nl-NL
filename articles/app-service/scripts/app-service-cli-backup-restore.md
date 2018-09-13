---
title: Azure CLI Script Sample - Restore a web app from a backup | Microsoft Docs
description: Azure CLI Script Sample - Restore a web app from a backup
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
ms.openlocfilehash: a7f292cfcfc90d3bacb245448b8e53d80488ebad
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868225"
---
# <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="6250b-103">Restore a web app from a backup</span><span class="sxs-lookup"><span data-stu-id="6250b-103">Restore a web app from a backup</span></span>

<span data-ttu-id="6250b-104">This sample script creates a web app in App Service with its related resources, and then creates a one-time backup for it.</span><span class="sxs-lookup"><span data-stu-id="6250b-104">This sample script creates a web app in App Service with its related resources, and then creates a one-time backup for it.</span></span> 

<span data-ttu-id="6250b-105">To run this script, you need an existing backup for a web app.</span><span class="sxs-lookup"><span data-stu-id="6250b-105">To run this script, you need an existing backup for a web app.</span></span> <span data-ttu-id="6250b-106">To create one, see [Backup up a web app](app-service-cli-backup-onetime.md) or [Create a scheduled backup for a web app](app-service-cli-backup-scheduled.md).</span><span class="sxs-lookup"><span data-stu-id="6250b-106">To create one, see [Backup up a web app](app-service-cli-backup-onetime.md) or [Create a scheduled backup for a web app](app-service-cli-backup-scheduled.md).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6250b-107">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="6250b-107">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6250b-108">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="6250b-108">To find the version, run `az --version`.</span></span> <span data-ttu-id="6250b-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6250b-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6250b-110">Sample script</span><span class="sxs-lookup"><span data-stu-id="6250b-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/backup-restore/backup-restore.sh?highlight=3-4,9 "Restore a web app from a backup")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6250b-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="6250b-111">Script explanation</span></span>

<span data-ttu-id="6250b-112">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="6250b-112">This script uses the following commands.</span></span> <span data-ttu-id="6250b-113">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="6250b-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6250b-114">Command</span><span class="sxs-lookup"><span data-stu-id="6250b-114">Command</span></span> | <span data-ttu-id="6250b-115">Notes</span><span class="sxs-lookup"><span data-stu-id="6250b-115">Notes</span></span> |
|---|---|
| [`az webapp config backup list`](/cli/azure/webapp/config/backup?view=azure-cli-latest#az-webapp-config-backup-list) | <span data-ttu-id="6250b-116">Gets a list of backups for a web app.</span><span class="sxs-lookup"><span data-stu-id="6250b-116">Gets a list of backups for a web app.</span></span> |
| [`az webapp config backup restore`](/cli/azure/webapp/config/backup?view=azure-cli-latest#az-webapp-config-backup-restore) | <span data-ttu-id="6250b-117">Restores a web app from a backup.</span><span class="sxs-lookup"><span data-stu-id="6250b-117">Restores a web app from a backup.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6250b-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="6250b-118">Next steps</span></span>

<span data-ttu-id="6250b-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="6250b-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="6250b-120">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6250b-120">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
