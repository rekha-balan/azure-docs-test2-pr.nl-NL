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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.openlocfilehash: 978e2b58898c2a4bcf48fc3f32c30596aa2e50d8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555768"
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="7f9c4-103">Monitor a web app with web server logs</span><span class="sxs-lookup"><span data-stu-id="7f9c4-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="7f9c4-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span><span class="sxs-lookup"><span data-stu-id="7f9c4-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="7f9c4-105">You will then download the log files for review.</span><span class="sxs-lookup"><span data-stu-id="7f9c4-105">You will then download the log files for review.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="7f9c4-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="7f9c4-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="7f9c4-107">Script explanation</span><span class="sxs-lookup"><span data-stu-id="7f9c4-107">Script explanation</span></span>

<span data-ttu-id="7f9c4-108">This script uses the following commands to create a resource group, web app, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="7f9c4-108">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="7f9c4-109">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="7f9c4-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7f9c4-110">Command</span><span class="sxs-lookup"><span data-stu-id="7f9c4-110">Command</span></span> | <span data-ttu-id="7f9c4-111">Notes</span><span class="sxs-lookup"><span data-stu-id="7f9c4-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7f9c4-112">az group create</span><span class="sxs-lookup"><span data-stu-id="7f9c4-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7f9c4-113">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="7f9c4-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7f9c4-114">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="7f9c4-114">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="7f9c4-115">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="7f9c4-115">Creates an App Service plan.</span></span> <span data-ttu-id="7f9c4-116">This is like a server farm for your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="7f9c4-116">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="7f9c4-117">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="7f9c4-117">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="7f9c4-118">Creates an Azure web app within the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="7f9c4-118">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="7f9c4-119">az appservice web log config</span><span class="sxs-lookup"><span data-stu-id="7f9c4-119">az appservice web log config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/log#config) | <span data-ttu-id="7f9c4-120">Configures which logs an Azure web app will persist.</span><span class="sxs-lookup"><span data-stu-id="7f9c4-120">Configures which logs an Azure web app will persist.</span></span> |
| [<span data-ttu-id="7f9c4-121">az appservice web log download</span><span class="sxs-lookup"><span data-stu-id="7f9c4-121">az appservice web log download</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/log#download) | <span data-ttu-id="7f9c4-122">Downloads the logs of the an Azure web app to your local machine.</span><span class="sxs-lookup"><span data-stu-id="7f9c4-122">Downloads the logs of the an Azure web app to your local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7f9c4-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="7f9c4-123">Next steps</span></span>

<span data-ttu-id="7f9c4-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7f9c4-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7f9c4-125">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7f9c4-125">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>