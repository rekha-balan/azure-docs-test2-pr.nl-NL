---
title: Azure CLI Script Sample - Connect a web app to documentdb | Microsoft Docs
description: Azure CLI Script Sample - Connect a web app to documentdb
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: bbbdbc42-efb5-4b4f-8ba6-c03c9d16a7ea
ms.service: app-service
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.openlocfilehash: 6335fae28c1198b9276ece651b8d90c82a209905
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550347"
---
# <a name="connect-a-web-app-to-a-documentdb"></a><span data-ttu-id="3ae9b-103">Connect a web app to a documentdb</span><span class="sxs-lookup"><span data-stu-id="3ae9b-103">Connect a web app to a documentdb</span></span>

<span data-ttu-id="3ae9b-104">In this scenario you will learn how to create an Azure documentdb and an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="3ae9b-104">In this scenario you will learn how to create an Azure documentdb and an Azure web app.</span></span> <span data-ttu-id="3ae9b-105">Then you will link the documentdb to the web app using app settings.</span><span class="sxs-lookup"><span data-stu-id="3ae9b-105">Then you will link the documentdb to the web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="3ae9b-106">Sample script</span><span class="sxs-lookup"><span data-stu-id="3ae9b-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure DocumentDB")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="3ae9b-107">Script explanation</span><span class="sxs-lookup"><span data-stu-id="3ae9b-107">Script explanation</span></span>

<span data-ttu-id="3ae9b-108">This script uses the following commands to create a resource group, web app, documentdb and all related resources.</span><span class="sxs-lookup"><span data-stu-id="3ae9b-108">This script uses the following commands to create a resource group, web app, documentdb and all related resources.</span></span> <span data-ttu-id="3ae9b-109">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="3ae9b-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3ae9b-110">Command</span><span class="sxs-lookup"><span data-stu-id="3ae9b-110">Command</span></span> | <span data-ttu-id="3ae9b-111">Notes</span><span class="sxs-lookup"><span data-stu-id="3ae9b-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3ae9b-112">az group create</span><span class="sxs-lookup"><span data-stu-id="3ae9b-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3ae9b-113">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="3ae9b-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3ae9b-114">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="3ae9b-114">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="3ae9b-115">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="3ae9b-115">Creates an App Service plan.</span></span> <span data-ttu-id="3ae9b-116">This is like a server farm for your Azure web app.</span><span class="sxs-lookup"><span data-stu-id="3ae9b-116">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="3ae9b-117">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="3ae9b-117">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="3ae9b-118">Creates an Azure web app within the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="3ae9b-118">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="3ae9b-119">az documentdb create</span><span class="sxs-lookup"><span data-stu-id="3ae9b-119">az documentdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/documentdb#create) | <span data-ttu-id="3ae9b-120">Creates a documentdb.</span><span class="sxs-lookup"><span data-stu-id="3ae9b-120">Creates a documentdb.</span></span> <span data-ttu-id="3ae9b-121">This is where the data will be stored.</span><span class="sxs-lookup"><span data-stu-id="3ae9b-121">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="3ae9b-122">az documentdb list-keys</span><span class="sxs-lookup"><span data-stu-id="3ae9b-122">az documentdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/documentdb#list-keys) | <span data-ttu-id="3ae9b-123">Lists the access keys for the specified Azure DocumentDB database account.</span><span class="sxs-lookup"><span data-stu-id="3ae9b-123">Lists the access keys for the specified Azure DocumentDB database account.</span></span> |
| [<span data-ttu-id="3ae9b-124">az appservice web config appsetings update</span><span class="sxs-lookup"><span data-stu-id="3ae9b-124">az appservice web config appsetings update</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) | <span data-ttu-id="3ae9b-125">Creates or updates an app setting for an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="3ae9b-125">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="3ae9b-126">App settings are exposed as environment variables for your app.</span><span class="sxs-lookup"><span data-stu-id="3ae9b-126">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3ae9b-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="3ae9b-127">Next steps</span></span>

<span data-ttu-id="3ae9b-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3ae9b-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3ae9b-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3ae9b-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>