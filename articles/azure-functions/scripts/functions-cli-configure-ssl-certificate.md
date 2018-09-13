---
title: Azure CLI Script Sample - Bind a custom SSL certificate to a function app | Microsoft Docs
description: Azure CLI Script Sample - Bind a custom SSL certificate to a function app in Azure
services: functions
documentationcenter: ''
author: ggailey777
manager: jeconnoc
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: azure-functions
ms.devlang: azurecli
ms.topic: sample
ms.date: 07/03/2013
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 8d8b96cec202edd1e93e9f7c04a5e508ed68a40e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865614"
---
# <a name="bind-a-custom-ssl-certificate-to-a-function-app"></a><span data-ttu-id="8bafd-103">Bind a custom SSL certificate to a function app</span><span class="sxs-lookup"><span data-stu-id="8bafd-103">Bind a custom SSL certificate to a function app</span></span>

<span data-ttu-id="8bafd-104">This sample script creates a function app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span><span class="sxs-lookup"><span data-stu-id="8bafd-104">This sample script creates a function app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="8bafd-105">For this sample, you need:</span><span class="sxs-lookup"><span data-stu-id="8bafd-105">For this sample, you need:</span></span>

* <span data-ttu-id="8bafd-106">Access to your domain registrar's DNS configuration page.</span><span class="sxs-lookup"><span data-stu-id="8bafd-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="8bafd-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span><span class="sxs-lookup"><span data-stu-id="8bafd-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>
* <span data-ttu-id="8bafd-108">Have configured an A record in your custom domain that points to your web app's default domain name.</span><span class="sxs-lookup"><span data-stu-id="8bafd-108">Have configured an A record in your custom domain that points to your web app's default domain name.</span></span> <span data-ttu-id="8bafd-109">For more information, see the [Map custom domain instructions for Azure App Service](https://aka.ms/appservicecustomdns).</span><span class="sxs-lookup"><span data-stu-id="8bafd-109">For more information, see the [Map custom domain instructions for Azure App Service](https://aka.ms/appservicecustomdns).</span></span>

<span data-ttu-id="8bafd-110">To bind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span><span class="sxs-lookup"><span data-stu-id="8bafd-110">To bind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8bafd-111">If you choose to install and use the CLI locally, you must be running the Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="8bafd-111">If you choose to install and use the CLI locally, you must be running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8bafd-112">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="8bafd-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="8bafd-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8bafd-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="8bafd-114">Sample script</span><span class="sxs-lookup"><span data-stu-id="8bafd-114">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="8bafd-115">Script explanation</span><span class="sxs-lookup"><span data-stu-id="8bafd-115">Script explanation</span></span>

<span data-ttu-id="8bafd-116">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="8bafd-116">This script uses the following commands.</span></span> <span data-ttu-id="8bafd-117">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="8bafd-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8bafd-118">Command</span><span class="sxs-lookup"><span data-stu-id="8bafd-118">Command</span></span> | <span data-ttu-id="8bafd-119">Notes</span><span class="sxs-lookup"><span data-stu-id="8bafd-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8bafd-120">az group create</span><span class="sxs-lookup"><span data-stu-id="8bafd-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#az-group-create) | <span data-ttu-id="8bafd-121">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="8bafd-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8bafd-122">az storage account create</span><span class="sxs-lookup"><span data-stu-id="8bafd-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#az-storage-account-create) | <span data-ttu-id="8bafd-123">Creates a storage account required by the function app.</span><span class="sxs-lookup"><span data-stu-id="8bafd-123">Creates a storage account required by the function app.</span></span> |
| [<span data-ttu-id="8bafd-124">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="8bafd-124">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#az-appservice-plan-create) | <span data-ttu-id="8bafd-125">Creates an App Service plan required to bind SSL certificates.</span><span class="sxs-lookup"><span data-stu-id="8bafd-125">Creates an App Service plan required to bind SSL certificates.</span></span> |
| [<span data-ttu-id="8bafd-126">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="8bafd-126">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#az-functionapp-create) | <span data-ttu-id="8bafd-127">Creates a function app in the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="8bafd-127">Creates a function app in the App Service plan.</span></span> |
| [<span data-ttu-id="8bafd-128">az functionapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="8bafd-128">az functionapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/functionapp/config/hostname#az-functionapp-config-hostname-add) | <span data-ttu-id="8bafd-129">Maps a custom domain to a function app.</span><span class="sxs-lookup"><span data-stu-id="8bafd-129">Maps a custom domain to a function app.</span></span> |
| [<span data-ttu-id="8bafd-130">az functionapp config ssl upload</span><span class="sxs-lookup"><span data-stu-id="8bafd-130">az functionapp config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/functionapp/config/ssl#az-functionapp-config-ssl-upload) | <span data-ttu-id="8bafd-131">Uploads an SSL certificate to a function app.</span><span class="sxs-lookup"><span data-stu-id="8bafd-131">Uploads an SSL certificate to a function app.</span></span> |
| [<span data-ttu-id="8bafd-132">az functionapp config ssl bind</span><span class="sxs-lookup"><span data-stu-id="8bafd-132">az functionapp config ssl bind</span></span>](https://docs.microsoft.com/cli/azure/functionapp/config/ssl#az-functionapp-config-ssl-bind) | <span data-ttu-id="8bafd-133">Binds an uploaded SSL certificate to a function app.</span><span class="sxs-lookup"><span data-stu-id="8bafd-133">Binds an uploaded SSL certificate to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8bafd-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="8bafd-134">Next steps</span></span>

<span data-ttu-id="8bafd-135">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="8bafd-135">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="8bafd-136">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8bafd-136">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../functions-cli-samples.md).</span></span>
