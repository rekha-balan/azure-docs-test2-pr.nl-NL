---
title: Azure CLI Script Sample - Connect a web app to a storage account | Microsoft Docs
description: Azure CLI Script Sample - Connect a web app to a storage account
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.openlocfilehash: 98396d532cb121c770ecfa5e3641d7665501de77
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669027"
---
# <a name="connect-a-web-app-to-a-storage-account"></a><span data-ttu-id="96f96-103">Connect a web app to a storage account</span><span class="sxs-lookup"><span data-stu-id="96f96-103">Connect a web app to a storage account</span></span>

<span data-ttu-id="96f96-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="96f96-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="96f96-105">Then you will link the storage account to the web app using app settings.</span><span class="sxs-lookup"><span data-stu-id="96f96-105">Then you will link the storage account to the web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="96f96-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="96f96-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/app-service/connect-to-storage/connect-to-storage.sh "Azure Storage")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="96f96-107">Script explanation</span><span class="sxs-lookup"><span data-stu-id="96f96-107">Script explanation</span></span>

<span data-ttu-id="96f96-108">This script uses the following commands to create a resource group, web app, storage account and all related resources.</span><span class="sxs-lookup"><span data-stu-id="96f96-108">This script uses the following commands to create a resource group, web app, storage account and all related resources.</span></span> <span data-ttu-id="96f96-109">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="96f96-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="96f96-110">Command</span><span class="sxs-lookup"><span data-stu-id="96f96-110">Command</span></span> | <span data-ttu-id="96f96-111">Notes</span><span class="sxs-lookup"><span data-stu-id="96f96-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="96f96-112">az group create</span><span class="sxs-lookup"><span data-stu-id="96f96-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="96f96-113">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="96f96-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="96f96-114">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="96f96-114">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="96f96-115">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="96f96-115">Creates an App Service plan.</span></span> <span data-ttu-id="96f96-116">This is like a server farm for your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="96f96-116">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="96f96-117">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="96f96-117">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="96f96-118">Creates an Azure web app within the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="96f96-118">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="96f96-119">az storage account create</span><span class="sxs-lookup"><span data-stu-id="96f96-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="96f96-120">Creates a storage account.</span><span class="sxs-lookup"><span data-stu-id="96f96-120">Creates a storage account.</span></span> <span data-ttu-id="96f96-121">This is where the static assets will be stored.</span><span class="sxs-lookup"><span data-stu-id="96f96-121">This is where the static assets will be stored.</span></span> |
| [<span data-ttu-id="96f96-122">az storage account show-connection-string</span><span class="sxs-lookup"><span data-stu-id="96f96-122">az storage account show-connection-string</span></span>](https://docs.microsoft.com/cli/azure/storage/account#show-connection-string) | |
| [<span data-ttu-id="96f96-123">az appservice web config appsetings update</span><span class="sxs-lookup"><span data-stu-id="96f96-123">az appservice web config appsetings update</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) | <span data-ttu-id="96f96-124">Creates or updates an app setting for an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="96f96-124">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="96f96-125">App settings are exposed as environment variables for your app.</span><span class="sxs-lookup"><span data-stu-id="96f96-125">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="96f96-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="96f96-126">Next steps</span></span>

<span data-ttu-id="96f96-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="96f96-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="96f96-128">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="96f96-128">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
