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
ms.topic: article
ms.date: 04/10/2017
ms.author: cephalin
ms.openlocfilehash: 34b4b89dc2492c8f12a49d521f7eb0ec73a339ba
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548893"
---
# <a name="bind-a-custom-ssl-certificate-to-a-web-app"></a><span data-ttu-id="9ea94-103">Bind a custom SSL certificate to a web app</span><span class="sxs-lookup"><span data-stu-id="9ea94-103">Bind a custom SSL certificate to a web app</span></span>

<span data-ttu-id="9ea94-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span><span class="sxs-lookup"><span data-stu-id="9ea94-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="9ea94-105">For this sample, you will need:</span><span class="sxs-lookup"><span data-stu-id="9ea94-105">For this sample, you will need:</span></span>

* <span data-ttu-id="9ea94-106">Access to your domain registrar's DNS configuration page.</span><span class="sxs-lookup"><span data-stu-id="9ea94-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="9ea94-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span><span class="sxs-lookup"><span data-stu-id="9ea94-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="9ea94-108">Sample script</span><span class="sxs-lookup"><span data-stu-id="9ea94-108">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="9ea94-109">Script explanation</span><span class="sxs-lookup"><span data-stu-id="9ea94-109">Script explanation</span></span>

<span data-ttu-id="9ea94-110">This script uses the following commands.</span><span class="sxs-lookup"><span data-stu-id="9ea94-110">This script uses the following commands.</span></span> <span data-ttu-id="9ea94-111">Each command in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="9ea94-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9ea94-112">Command</span><span class="sxs-lookup"><span data-stu-id="9ea94-112">Command</span></span> | <span data-ttu-id="9ea94-113">Notes</span><span class="sxs-lookup"><span data-stu-id="9ea94-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9ea94-114">az group create</span><span class="sxs-lookup"><span data-stu-id="9ea94-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9ea94-115">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="9ea94-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9ea94-116">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="9ea94-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="9ea94-117">Creates an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="9ea94-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="9ea94-118">az appservice web create</span><span class="sxs-lookup"><span data-stu-id="9ea94-118">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="9ea94-119">Creates an Azure web app.</span><span class="sxs-lookup"><span data-stu-id="9ea94-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="9ea94-120">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="9ea94-120">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="9ea94-121">Maps a custom domain to a web app.</span><span class="sxs-lookup"><span data-stu-id="9ea94-121">Maps a custom domain to a web app.</span></span> |
| [<span data-ttu-id="9ea94-122">az appservice web config ssl upload</span><span class="sxs-lookup"><span data-stu-id="9ea94-122">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="9ea94-123">Uploads an SSL certificate to a web app.</span><span class="sxs-lookup"><span data-stu-id="9ea94-123">Uploads an SSL certificate to a web app.</span></span> |
| [<span data-ttu-id="9ea94-124">az appservice web config ssl bind</span><span class="sxs-lookup"><span data-stu-id="9ea94-124">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="9ea94-125">Binds an uploaded SSL certificate to a web app.</span><span class="sxs-lookup"><span data-stu-id="9ea94-125">Binds an uploaded SSL certificate to a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9ea94-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="9ea94-126">Next steps</span></span>

<span data-ttu-id="9ea94-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9ea94-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9ea94-128">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9ea94-128">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
