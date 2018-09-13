---
title: Azure CLI Script Sample - Monitor a web app with web server logs | Microsoft Docs
description: Azure CLI Script Sample - Monitor a web app with web server logs
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 0887656f-611c-4627-8247-b5cded7cef60
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 12/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: dc9bc90eb5be6fd700f5a7ca4cbac28170633722
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865123"
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="695f7-103">Monitor a web app with web server logs</span><span class="sxs-lookup"><span data-stu-id="695f7-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="695f7-104">This sample script creates a resource group, app service plan, and web app, and configures the web app to enable web server logs.</span><span class="sxs-lookup"><span data-stu-id="695f7-104">This sample script creates a resource group, app service plan, and web app, and configures the web app to enable web server logs.</span></span> <span data-ttu-id="695f7-105">It then downloads the log files for review.</span><span class="sxs-lookup"><span data-stu-id="695f7-105">It then downloads the log files for review.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="695f7-106">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="695f7-106">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="695f7-107">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="695f7-107">To find the version, run `az --version`.</span></span> <span data-ttu-id="695f7-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="695f7-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="sample-script"></a><span data-ttu-id="695f7-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="695f7-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="695f7-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="695f7-110">Script explanation</span></span>

<span data-ttu-id="695f7-111">This script uses the following commands to create a resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="695f7-111">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="695f7-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="695f7-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="695f7-113">Command</span><span class="sxs-lookup"><span data-stu-id="695f7-113">Command</span></span> | <span data-ttu-id="695f7-114">Notes</span><span class="sxs-lookup"><span data-stu-id="695f7-114">Notes</span></span> |
|---|---|
| [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) | <span data-ttu-id="695f7-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="695f7-115">Creates a resource group in which all resources are stored.</span></span> |
| [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) | <span data-ttu-id="695f7-116">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="695f7-116">Creates an App Service plan.</span></span> |
| [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) | <span data-ttu-id="695f7-117">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="695f7-117">Creates an Azure web app.</span></span> |
| [`az webapp log config`](/cli/azure/webapp/log?view=azure-cli-latest#az-webapp-log-config) | <span data-ttu-id="695f7-118">Configures which logs an Azure web app persists.</span><span class="sxs-lookup"><span data-stu-id="695f7-118">Configures which logs an Azure web app persists.</span></span> |
| [`az webapp log download`](/cli/azure/webapp/log?view=azure-cli-latest#az-webapp-log-download) | <span data-ttu-id="695f7-119">Downloads the logs of an Azure web app to your local machine.</span><span class="sxs-lookup"><span data-stu-id="695f7-119">Downloads the logs of an Azure web app to your local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="695f7-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="695f7-120">Next steps</span></span>

<span data-ttu-id="695f7-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="695f7-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="695f7-122">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="695f7-122">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
