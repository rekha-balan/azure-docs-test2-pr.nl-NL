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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.openlocfilehash: c576157f2c641a916f7b595fe0d2d1c0af2c0066
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662199"
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="f93de-103">Connect a web app to a SQL database</span><span class="sxs-lookup"><span data-stu-id="f93de-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="f93de-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="f93de-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="f93de-105">Then you will link the SQL database to the web app using app settings.</span><span class="sxs-lookup"><span data-stu-id="f93de-105">Then you will link the SQL database to the web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="f93de-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="f93de-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f93de-107">Script explanation</span><span class="sxs-lookup"><span data-stu-id="f93de-107">Script explanation</span></span>

<span data-ttu-id="f93de-108">This script uses the following commands to create a resource group, web app, SQL database and all related resources.</span><span class="sxs-lookup"><span data-stu-id="f93de-108">This script uses the following commands to create a resource group, web app, SQL database and all related resources.</span></span> <span data-ttu-id="f93de-109">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="f93de-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f93de-110">Command</span><span class="sxs-lookup"><span data-stu-id="f93de-110">Command</span></span> | <span data-ttu-id="f93de-111">Notes</span><span class="sxs-lookup"><span data-stu-id="f93de-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f93de-112">az group create</span><span class="sxs-lookup"><span data-stu-id="f93de-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f93de-113">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="f93de-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f93de-114">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="f93de-114">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="f93de-115">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="f93de-115">Creates an App Service plan.</span></span> <span data-ttu-id="f93de-116">This is like a server farm for your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="f93de-116">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="f93de-117">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="f93de-117">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="f93de-118">Creates an Azure web app within the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="f93de-118">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="f93de-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="f93de-119">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="f93de-120">Creates a SQL Database Server.</span><span class="sxs-lookup"><span data-stu-id="f93de-120">Creates a SQL Database Server.</span></span>  |
| [<span data-ttu-id="f93de-121">az sql db create</span><span class="sxs-lookup"><span data-stu-id="f93de-121">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="f93de-122">Creates a new database with the SQL Database Server.</span><span class="sxs-lookup"><span data-stu-id="f93de-122">Creates a new database with the SQL Database Server.</span></span> |
| [<span data-ttu-id="f93de-123">az appservice web config appsetings update</span><span class="sxs-lookup"><span data-stu-id="f93de-123">az appservice web config appsetings update</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) | <span data-ttu-id="f93de-124">Creates or updates an app setting for an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="f93de-124">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="f93de-125">App settings are exposed as environment variables for your app.</span><span class="sxs-lookup"><span data-stu-id="f93de-125">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f93de-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="f93de-126">Next steps</span></span>

<span data-ttu-id="f93de-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f93de-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f93de-128">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f93de-128">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>