---
title: Azure CLI Script Sample - Connect a web app to MongoDB (Cosmos DB) | Microsoft Docs
description: Azure CLI Script Sample - Connect a web app to MongoDB (Cosmos DB)
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: bbbdbc42-efb5-4b4f-8ba6-c03c9d16a7ea
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 12/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: f2b486e32cef87e3f06727f46c9741b4db546d18
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857063"
---
# <a name="connect-a-web-app-to-cosmos-db"></a><span data-ttu-id="c138c-103">Connect a web app to Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c138c-103">Connect a web app to Cosmos DB</span></span>

<span data-ttu-id="c138c-104">This sample script creates an Azure Cosmos DB account with the MongoDB API and an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="c138c-104">This sample script creates an Azure Cosmos DB account with the MongoDB API and an Azure web app.</span></span> <span data-ttu-id="c138c-105">It then links the MongoDB connection string to the web app using app settings.</span><span class="sxs-lookup"><span data-stu-id="c138c-105">It then links the MongoDB connection string to the web app using app settings.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c138c-106">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="c138c-106">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c138c-107">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="c138c-107">To find the version, run `az --version`.</span></span> <span data-ttu-id="c138c-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c138c-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="sample-script"></a><span data-ttu-id="c138c-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="c138c-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="c138c-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="c138c-110">Script explanation</span></span>

<span data-ttu-id="c138c-111">This script uses the following commands to create a resource group, web app, Cosmos DB, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="c138c-111">This script uses the following commands to create a resource group, web app, Cosmos DB, and all related resources.</span></span> <span data-ttu-id="c138c-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="c138c-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c138c-113">Command</span><span class="sxs-lookup"><span data-stu-id="c138c-113">Command</span></span> | <span data-ttu-id="c138c-114">Notes</span><span class="sxs-lookup"><span data-stu-id="c138c-114">Notes</span></span> |
|---|---|
| [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) | <span data-ttu-id="c138c-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="c138c-115">Creates a resource group in which all resources are stored.</span></span> |
| [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) | <span data-ttu-id="c138c-116">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="c138c-116">Creates an App Service plan.</span></span> |
| [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) | <span data-ttu-id="c138c-117">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="c138c-117">Creates an Azure web app.</span></span> |
| [`az cosmosdb create`](/cli/azure/cosmosdb?view=azure-cli-latest#az-cosmosdb-create) | <span data-ttu-id="c138c-118">Creates a Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="c138c-118">Creates a Cosmos DB account.</span></span> |
| [`az cosmosdb list-connection-strings`](/cli/azure/cosmosdb?view=azure-cli-latest#az-cosmosdb-list-connection-strings) | <span data-ttu-id="c138c-119">Lists connection strings for the specified Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="c138c-119">Lists connection strings for the specified Cosmos DB account.</span></span> |
| [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) | <span data-ttu-id="c138c-120">Creates or updates an app setting for an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="c138c-120">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="c138c-121">App settings are exposed as environment variables for your app.</span><span class="sxs-lookup"><span data-stu-id="c138c-121">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c138c-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="c138c-122">Next steps</span></span>

<span data-ttu-id="c138c-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="c138c-123">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="c138c-124">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c138c-124">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
