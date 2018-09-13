---
title: Create an Azure Function that connects to an Azure Cosmos DB | Microsoft Docs
description: Azure CLI Script Sample - Create an Azure Function that connects to an Azure Cosmos DB
services: functions
documentationcenter: functions
author: ggailey777
manager: jeconnoc
ms.assetid: ''
ms.service: azure-functions
ms.devlang: azurecli
ms.topic: sample
ms.date: 07/03/2018
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 6001fc5737ee901ab1ab5af0dd2f913f05380ac2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868533"
---
# <a name="create-an-azure-function-that-connects-to-an-azure-cosmos-db"></a><span data-ttu-id="7be76-103">Create an Azure Function that connects to an Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7be76-103">Create an Azure Function that connects to an Azure Cosmos DB</span></span>

<span data-ttu-id="7be76-104">This Azure Functions sample script creates a function app and connects the function to an Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="7be76-104">This Azure Functions sample script creates a function app and connects the function to an Azure Cosmos DB database.</span></span> <span data-ttu-id="7be76-105">The created app setting that contains the connection can be used with an [Azure Cosmos DB trigger or binding](..\functions-bindings-cosmosdb.md).</span><span class="sxs-lookup"><span data-stu-id="7be76-105">The created app setting that contains the connection can be used with an [Azure Cosmos DB trigger or binding](..\functions-bindings-cosmosdb.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7be76-106">If you use the CLI locally, make sure that you are running the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="7be76-106">If you use the CLI locally, make sure that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7be76-107">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="7be76-107">To find the version, run `az --version`.</span></span> <span data-ttu-id="7be76-108">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7be76-108">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="7be76-109">Sample script</span><span class="sxs-lookup"><span data-stu-id="7be76-109">Sample script</span></span>

<span data-ttu-id="7be76-110">This sample creates an Azure Function app and adds a Cosmos DB endpoint and access key to app settings.</span><span class="sxs-lookup"><span data-stu-id="7be76-110">This sample creates an Azure Function app and adds a Cosmos DB endpoint and access key to app settings.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects to an Azure Cosmos DB")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="7be76-111">Script explanation</span><span class="sxs-lookup"><span data-stu-id="7be76-111">Script explanation</span></span>

<span data-ttu-id="7be76-112">This script uses the following commands: Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="7be76-112">This script uses the following commands: Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7be76-113">Command</span><span class="sxs-lookup"><span data-stu-id="7be76-113">Command</span></span> | <span data-ttu-id="7be76-114">Notes</span><span class="sxs-lookup"><span data-stu-id="7be76-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7be76-115">az group create</span><span class="sxs-lookup"><span data-stu-id="7be76-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-create) | <span data-ttu-id="7be76-116">Create a resource group with location</span><span class="sxs-lookup"><span data-stu-id="7be76-116">Create a resource group with location</span></span> |
| [<span data-ttu-id="7be76-117">az storage accounts create</span><span class="sxs-lookup"><span data-stu-id="7be76-117">az storage accounts create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#az-storage-account-create) | <span data-ttu-id="7be76-118">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="7be76-118">Create a storage account</span></span> |
| [<span data-ttu-id="7be76-119">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="7be76-119">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#az-functionapp-create) | <span data-ttu-id="7be76-120">Creates a function app in the serverless [consumption plan](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="7be76-120">Creates a function app in the serverless [consumption plan](../functions-scale.md#consumption-plan).</span></span> |
| [<span data-ttu-id="7be76-121">az cosmosdb create</span><span class="sxs-lookup"><span data-stu-id="7be76-121">az cosmosdb create</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#az-cosmosdb-create) | <span data-ttu-id="7be76-122">Create an Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="7be76-122">Create an Azure Cosmos DB database.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7be76-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="7be76-123">Next steps</span></span>

<span data-ttu-id="7be76-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="7be76-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="7be76-125">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7be76-125">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>




