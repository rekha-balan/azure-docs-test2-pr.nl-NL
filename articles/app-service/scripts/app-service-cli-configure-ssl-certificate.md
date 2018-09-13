---
title: Azure CLI Script Sample - Bind a custom SSL certificate to a web app | Microsoft Docs
description: Azure CLI Script Sample - Bind a custom SSL certificate to a web app
services: app-service\web
documentationcenter: ''
author: cephalin
manager: erikre
editor: ''
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 12/11/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: f806b523543657e4241ec5bfbb4b84b85ebd9355
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868634"
---
# <a name="bind-a-custom-ssl-certificate-to-a-web-app"></a><span data-ttu-id="6dfa7-103">Bind a custom SSL certificate to a web app</span><span class="sxs-lookup"><span data-stu-id="6dfa7-103">Bind a custom SSL certificate to a web app</span></span>

<span data-ttu-id="6dfa7-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span><span class="sxs-lookup"><span data-stu-id="6dfa7-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="6dfa7-105">For this sample, you need:</span><span class="sxs-lookup"><span data-stu-id="6dfa7-105">For this sample, you need:</span></span>

* <span data-ttu-id="6dfa7-106">Access to your domain registrar's DNS configuration page.</span><span class="sxs-lookup"><span data-stu-id="6dfa7-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="6dfa7-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span><span class="sxs-lookup"><span data-stu-id="6dfa7-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6dfa7-108">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span><span class="sxs-lookup"><span data-stu-id="6dfa7-108">If you choose to install and use the CLI locally, you need Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6dfa7-109">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="6dfa7-109">To find the version, run `az --version`.</span></span> <span data-ttu-id="6dfa7-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6dfa7-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="sample-script"></a><span data-ttu-id="6dfa7-111">Sample script</span><span class="sxs-lookup"><span data-stu-id="6dfa7-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6dfa7-112">Script explanation</span><span class="sxs-lookup"><span data-stu-id="6dfa7-112">Script explanation</span></span>

<span data-ttu-id="6dfa7-113">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="6dfa7-113">This script uses the following commands.</span></span> <span data-ttu-id="6dfa7-114">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="6dfa7-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6dfa7-115">Command</span><span class="sxs-lookup"><span data-stu-id="6dfa7-115">Command</span></span> | <span data-ttu-id="6dfa7-116">Notes</span><span class="sxs-lookup"><span data-stu-id="6dfa7-116">Notes</span></span> |
|---|---|
| [`az group create`](/cli/azure/group?view=azure-cli-latest#az-group-create) | <span data-ttu-id="6dfa7-117">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="6dfa7-117">Creates a resource group in which all resources are stored.</span></span> |
| [`az appservice plan create`](/cli/azure/appservice/plan?view=azure-cli-latest#az-appservice-plan-create) | <span data-ttu-id="6dfa7-118">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="6dfa7-118">Creates an App Service plan.</span></span> |
| [`az webapp create`](/cli/azure/webapp?view=azure-cli-latest#az-webapp-create) | <span data-ttu-id="6dfa7-119">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="6dfa7-119">Creates an Azure web app.</span></span> |
| [`az webapp config hostname add`](/cli/azure/webapp/config/hostname?view=azure-cli-latest#az-webapp-config-hostname-add) | <span data-ttu-id="6dfa7-120">Maps a custom domain to a web app.</span><span class="sxs-lookup"><span data-stu-id="6dfa7-120">Maps a custom domain to a web app.</span></span> |
| [`az webapp config ssl upload`](/cli/azure/webapp/config/ssl?view=azure-cli-latest#az-webapp-config-ssl-upload) | <span data-ttu-id="6dfa7-121">Uploads an SSL certificate to a web app.</span><span class="sxs-lookup"><span data-stu-id="6dfa7-121">Uploads an SSL certificate to a web app.</span></span> |
| [`az webapp config ssl bind`](/cli/azure/webapp/config/ssl?view=azure-cli-latest#az-webapp-config-ssl-bind) | <span data-ttu-id="6dfa7-122">Binds an uploaded SSL certificate to a web app.</span><span class="sxs-lookup"><span data-stu-id="6dfa7-122">Binds an uploaded SSL certificate to a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6dfa7-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="6dfa7-123">Next steps</span></span>

<span data-ttu-id="6dfa7-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span><span class="sxs-lookup"><span data-stu-id="6dfa7-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure).</span></span>

<span data-ttu-id="6dfa7-125">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6dfa7-125">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
