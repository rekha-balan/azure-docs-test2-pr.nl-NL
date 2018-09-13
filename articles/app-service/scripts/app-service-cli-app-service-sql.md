---
title: Azure CLI Script Sample - Connect a web app to a SQL database | Microsoft Docs
description: Azure CLI Script Sample - Connect a web app to a SQL database
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: 7c2efdd0-f553-4038-a77a-e953021b3f77
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 12/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c9e50a965d07d8ab5c69e53d3f43cec9387274e8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866404"
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="4254b-103">Connect a web app to a SQL database</span><span class="sxs-lookup"><span data-stu-id="4254b-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="4254b-104">This sample script creates an Azure SQL database and an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="4254b-104">This sample script creates an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="4254b-105">It then links the SQL database to the web app using app settings.</span><span class="sxs-lookup"><span data-stu-id="4254b-105">It then links the SQL database to the web app using app settings.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4254b-106">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="4254b-106">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4254b-107">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="4254b-107">To find the version, run `az --version`.</span></span> <span data-ttu-id="4254b-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4254b-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="sample-script"></a><span data-ttu-id="4254b-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="4254b-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="4254b-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="4254b-110">Script explanation</span></span>

<span data-ttu-id="4254b-111">This script uses the following commands to create a resource group, web app, SQL Database, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="4254b-111">This script uses the following commands to create a resource group, web app, SQL Database, and all related resources.</span></span> <span data-ttu-id="4254b-112">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="4254b-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4254b-113">Command</span><span class="sxs-lookup"><span data-stu-id="4254b-113">Command</span></span> | <span data-ttu-id="4254b-114">Notes</span><span class="sxs-lookup"><span data-stu-id="4254b-114">Notes</span></span> |
|---|---|
| [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) | <span data-ttu-id="4254b-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="4254b-115">Creates a resource group in which all resources are stored.</span></span> |
| [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) | <span data-ttu-id="4254b-116">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="4254b-116">Creates an App Service plan.</span></span> |
| [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) | <span data-ttu-id="4254b-117">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="4254b-117">Creates an Azure web app.</span></span> |
| [`az sql server create`](/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-create) | <span data-ttu-id="4254b-118">Creates a SQL Database Server.</span><span class="sxs-lookup"><span data-stu-id="4254b-118">Creates a SQL Database Server.</span></span>  |
| [`az sql db create`](/cli/azure/sql/db?view=azure-cli-latest#az-sql-db-create) | <span data-ttu-id="4254b-119">Creates a new database with the SQL Database Server.</span><span class="sxs-lookup"><span data-stu-id="4254b-119">Creates a new database with the SQL Database Server.</span></span> |
| [`az sql db show-connection-string`](/cli/azure/sql/db?view=azure-cli-latest#az-sql-db-show-connection-string) | <span data-ttu-id="4254b-120">Generates a connection string to a database.</span><span class="sxs-lookup"><span data-stu-id="4254b-120">Generates a connection string to a database.</span></span> |
| [`az webapp config appsettings set`](/cli/azure/webapp/config/appsettings?view=azure-cli-latest#az-webapp-config-appsettings-set) | <span data-ttu-id="4254b-121">Creates or updates an app setting for an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="4254b-121">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="4254b-122">App settings are exposed as environment variables for your app.</span><span class="sxs-lookup"><span data-stu-id="4254b-122">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4254b-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="4254b-123">Next steps</span></span>

<span data-ttu-id="4254b-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="4254b-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="4254b-125">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4254b-125">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
